
# NAS가 MLflow 서버 역할까지 하려면 최소 사양
- MLflow 자체는 엄청 가벼워요. Python + SQLite만 있으면 돌아감

**MLflow 서버로 쓸 때 NAS 요구사항**

| 항목 | 최소 | 권장 |
|---|---|---|
| CPU | 1코어 이상 | 2코어 |
| RAM | **1GB** | 2GB |
| 저장공간 | 가중치 용량 + 여유 | SSD 권장 |
| OS | Linux 가능해야 함 | Ubuntu/Debian |
| 네트워크 | 로컬 접근 가능 | 고정 IP |


---


# 구조 
```
[게임 환경]  →  state (위치, 속도, 각도 등)  →  [AI 모델 (Policy)]
    ↑                                                      ↓
reward (명중/회피)  ←←←←←←←←  action (방향, 가속 등)

```

- 에피소드마다 (state, action, reward, next_state, done)  →  Replay Buffer

|구분|내용|
|---|---|
|코드|모델 구조, 알고리즘 (PPO/DQN 등), 리워드 설계|
|환경 설정|게임 파라미터 (미사일 속도, 맵 크기 등)|
|모델|학습된 가중치 (.pt 파일)|
|플레이 데이터|Replay Buffer (state/action/reward 시퀀스)|
|결과|episode reward, 명중률 등|


# 기록 내용 
git_dirty : 커밋되지 않은 변경사항 존재 여부
- 실험 돌릴 때 커밋을 깜빡하면 나중에 "이 결과 어떤 코드로 나온 거지?"

# 학습 중 메트릭 로깅 (RL 특화)
```
for episode in range(num_episodes):
    episode_reward, episode_len, loss = train_one_episode(...)
    
    mlflow.log_metrics({
        "episode_reward": episode_reward,
        "episode_length": episode_len,
        "policy_loss": loss["policy"],
        "value_loss": loss["value"],
        "entropy": loss["entropy"],
    }, step=episode)
    
    # 100 에피소드마다 이동평균도 같이 (수렴 판단에 유용)
    if episode % 100 == 0:
        mlflow.log_metric("reward_ma100", moving_avg, step=episode)
```


3. 체크포인트 + 학습 설정 묶어서 관리
```
import torch
import yaml

def save_checkpoint(model, optimizer, episode, config, path="checkpoint.pt"):
    torch.save({
        "model_state": model.state_dict(),
        "optimizer_state": optimizer.state_dict(),
        "episode": episode,
        "config": config,  # 하이퍼파라미터 통째로 같이 저장
    }, path)
    mlflow.log_artifact(path, artifact_path="checkpoints")

# 학습 중간중간
save_checkpoint(model, optimizer, episode, config, f"ckpt_ep{episode}.pt")

# 최종 모델은 MLflow 표준 포맷으로도 저장 (나중에 mlflow.pytorch.load_model로 바로 불러오기 가능)
mlflow.pytorch.log_model(model, "final_model")
```



# 사용 
UI에서 git_commit 태그로 필터링하면 "이 코드 버전으로 돌린 실험들"만 모아볼 수 있고, 파라미터 컬럼 정렬해서 하이퍼파라미터 스윕 결과 비교도 바로



# 최종 구조 
```
GitLab
└── 코드 버전관리 (commit hash가 연결고리)

Synology NAS
├── Docker: MLflow 서버 (실험 추적/인덱스)
└── 가중치 파일 저장소 (NAS 볼륨 마운트)

개발 PC
└── train.py 실행 → MLflow에 자동 기록
```



데이터는 nas에 저장되는거 맞지? 

저장시점은?


# 1. 로컬 기본 가중치로 시연
python play.py

# 2. 특정 체크포인트로 시연 (중간 가중치 비교)
python play.py --model checkpoints/rocket_ckpt_50000_steps

# 3. MLflow 대시보드에서 run_id 복사해서 NAS에서 직접 불러오기
python play.py --run-id abc123def456 --artifact final_model/trained_3d_rocket.zip

# 4. 긴급 저장된 가중치로 시연
python play.py --run-id abc123def456 --artifact emergency/trained_3d_rocket_emergency.zip



python play.py --run-id <run_id> --artifact final_model/trained_3d_rocket.zip


# 저장 매커니즘
- SB3는 model.save()를 하면 .zip 파일 하나로 저장
- 정책 네트워크 가중치 + 옵티마이저 상태 + 하이퍼파라미터가 다 포함


# 로드해서 쓰기

```

import mlflow
from stable_baselines3 import PPO

# 1) 최고 run의 가중치 다운로드
best_run_id = "abc123..."  # 이전 답변의 search_runs로 찾은 run_id
local_path = mlflow.artifacts.download_artifacts(
    run_id=best_run_id,
    artifact_path="model/ppo_missile_final.zip"
)

# 2) SB3 모델 객체로 복원
model = PPO.load(local_path)

```

# 게임 루프에서 사용 
```
obs = env.reset()
while True:
    action, _states = model.predict(obs, deterministic=True)  # 추론이므로 deterministic
    obs, reward, done, info = env.step(action)
    if done:
        obs = env.reset()

```

- deterministic=True
  - 학습 때는 탐험을 위해 확률적으로 행동을 뽑지만(stochastic), 실제 게임에 배포할 때는 매번 최선의 행동만 나오도록 이렇게 설정

- model.predict()
  - 환경(env)과 상호작용할 준비가 된 형태로 obs를 넣으면 action을 뱉어줌
  - 학습 때 쓴 obs 전처리(정규화 등)와 반드시 동일한 형태여야 함
   - 주의 : 예: VecNormalize를 학습 때 썼으면 추론 때도 그 통계값을 같이 로드해야 함


## VecNormalize

RL 환경 wrapping에서 VecNormalize로 관측값을 정규화했다면, 그 통계(running mean/std)도 같이 저장/로드해야 정확히 재현


```
# 저장 시
env.save("/tmp/vecnormalize.pkl")
mlflow.log_artifact("/tmp/vecnormalize.pkl", artifact_path="model")

# 로드 시
from stable_baselines3.common.vec_env import VecNormalize
env = VecNormalize.load(downloaded_vecnormalize_path, base_env)
env.training = False  # 추론 모드에서는 통계 업데이트 중단
env.norm_reward = False

```




# 사용시나리오 1 - 처음 학습 시작

1. config.yaml에 하이퍼파라미터 설정
   (lr, gamma, 네트워크 구조 등)

2. train.py 실행
   → MLflow가 자동으로:
      - git commit hash 기록
      - config.yaml 파라미터 기록
      - 학습 시작 시간 기록

3. 학습 진행 중
   → 에피소드마다 reward, loss 대시보드에 실시간 기록

4. 학습 완료
   → 가중치 NAS에 자동 저장
   → 대시보드에서 결과 확인



# 시나리오 2 - 하이퍼파라미터 바꿔서 비교 실험
1. config.yaml에서 lr만 바꿈 (3e-4 → 1e-4)

2. train.py 다시 실행
   → MLflow에 새 run으로 기록

3. 대시보드에서 두 실험 나란히 비교
   ├── run_001: lr=3e-4, reward=85
   └── run_002: lr=1e-4, reward=92  ← 이게 더 좋네!

4. run_002 가중치로 시뮬레이터 실행

# 시나리오 3 - 좋은 가중치로 게임 실행

1. 대시보드에서 reward 높은 run 선택
2. 해당 run의 가중치 경로 확인
3. play.py 실행
   → 가중치 로드 → 시뮬레이터 실행 → AI가 게임 플레이

# 시나리오 4 - 나중에 재현

1. 대시보드에서 예전 실험 클릭
2. git_commit hash 확인
3. git checkout <hash>
4. 동일한 가중치 로드
   → 완전히 똑같은 결과 재현 가능