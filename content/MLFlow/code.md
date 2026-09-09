```
mlflow.set_tracking_uri("http://192.168.1.236:5050") # mlflow url 주소 
mlflow.set_experiment("model-1") # 실험 이름 설정
mlflow.start_run()        # 실행 시작
mlflow.log_params()       # 하이퍼파라미터 기록
mlflow.log_metrics()      # 학습 결과 기록
mlflow.log_artifact()     # 가중치 파일 기록
```



# 예제 
```
def main():
    mlflow.set_tracking_uri("http://192.168.1.236:5050")
    mlflow.set_experiment("model-1")

    # ✅ 여기서 run 시작
    with mlflow.start_run(run_name=f"ppo_{args.timesteps}steps"):
        
        # ✅ 하이퍼파라미터 기록
        mlflow.log_params({
            "algo": "PPO",
            "policy": "MlpPolicy",
            "learning_rate": 0.001,
            "gamma": 0.99,
            "num_cpu": 8,
            "timesteps": args.timesteps,
            "pi_arch": "[128, 128]",
            "vf_arch": "[256, 256]",
            "activation": "ReLU",
            "boost_time": 5.0,
            "init_pitch": 30.0,
        })

        # 기존 모델 로드 or 신규 생성 코드 그대로...
        
        # ✅ 학습 콜백으로 메트릭 기록 (아래 설명 참고)
        model.learn(
            total_timesteps=args.timesteps,
            reset_num_timesteps=False,
            callback=MLflowCallback()  # ✅ 추가
        )
        
        # ✅ 가중치 저장 후 MLflow에도 업로드
        model.save(model_filename)
        mlflow.log_artifact(f"{model_filename}.zip")
        print("💾 학습 완료 및 MLflow 기록 완료!")

```

# 콜백 클래스 
```
class MLflowCallback(BaseCallback):
    def __init__(self, log_interval=1000):
        super().__init__()
        self.log_interval = log_interval

    def _on_step(self) -> bool:
        if self.n_calls % self.log_interval == 0:
            # SB3가 자동으로 계산하는 메트릭 가져오기
            if len(self.model.ep_info_buffer) > 0:
                ep_rewards = [ep["r"] for ep in self.model.ep_info_buffer]
                ep_lens = [ep["l"] for ep in self.model.ep_info_buffer]
                mlflow.log_metrics({
                    "mean_reward": sum(ep_rewards) / len(ep_rewards),
                    "mean_ep_length": sum(ep_lens) / len(ep_lens),
                }, step=self.num_timesteps)
        return True
```

# 테스트 가이드라인

**1단계 - 기준 실험 (Baseline) 잡기**

```
실험명: ppo_baseline
timesteps: 50,000
현재 설정 그대로 돌리기
→ 대시보드에서 mean_reward 추이 확인
→ 수렴하는지 / 발산하는지 파악
```

**2단계 - 하이퍼파라미터 하나씩만 바꾸기**

```
실험 2: learning_rate 0.001 → 3e-4
실험 3: pi_arch [128,128] → [256,256]
실험 4: num_cpu 8 → 4
→ baseline 대비 mean_reward 비교
```

**3단계 - 대시보드에서 비교**

```
http://192.168.1.236:5050
→ missile-rl 실험 클릭
→ 여러 run 체크박스 선택
→ Compare 버튼
→ reward 커브 나란히 비교
```

**4단계 - 좋은 가중치로 시연**

```
대시보드에서 reward 높은 run 선택
→ Artifacts 탭에서 .zip 경로 확인
→ play.py에서 해당 경로로 로드
→ render_mode="human" 으로 시연
```

---

**미션 결과도 기록하면 더 좋아요**

`rocket_tracking_sim.py`의 `step()` 마지막에 `mission_result`가 있으니, 에피소드 종료 시 결과도 MLflow에 기록할 수 있어요:

```python
# 콜백에서 에피소드 종료 감지
if terminated or truncated:
    if env.mission_result:
        status = env.mission_result["status"]
        mlflow.log_metric("hit_rate", 1.0 if "HIT" in status else 0.0, 
                         step=self.num_timesteps)
```



# 실제 구성 

rocket_tracking_sim.py  →  환경 (게임 규칙, 물리, 렌더링)
train.py                →  학습 (모델 생성, 학습 루프, 결과 기록)

MLflow는 "학습 실험을 추적" 하는 도구



❌ 문제점
- 환경을 다른 프로젝트에서 재사용할 때 MLflow가 딸려옴
- 환경이 학습 추적 도구에 의존하게 됨 (관심사 분리 위반)
- SubprocVecEnv로 병렬 실행할 때 각 프로세스마다 
  MLflow 연결 시도 → 충돌 가능성


# 저장
```
Git Commit (코드)
    → 개발자가 수동으로 하는 것
    → 학습 전에 코드 확정하고 커밋
    → 자동이 아님!

NAS 가중치 저장 (MLflow)
    → 학습 중/후 자동으로 올라감
    → 10000스텝마다 체크포인트
    → 학습 완료 시 최종 저장
```

## 가중치 저장 
```
학습 완료
    ↓
로컬 PC에 .zip 저장
    ↓
MLflow가 NAS로 복사
    ↓
NAS /volume1/docker/mlflow/artifacts/ 에 보관
```


```
# train.py
model.learn(total_timesteps=args.timesteps)  # 학습 완료 후

model.save(model_filename)  # ← 여기서 로컬 PC에 저장, trained_3d_rocket.zip 생성

mlflow.log_artifact(f"{model_filename}.zip")  # ← 여기서 NAS로 업로드

```

## 중간 체크포인트 저장

```
from stable_baselines3.common.callbacks import CheckpointCallback

checkpoint_callback = CheckpointCallback(
    save_freq=10000,          # 1만 스텝마다
    save_path="./checkpoints/",
    name_prefix="rocket_ckpt"
)

model.learn(
    total_timesteps=args.timesteps,
    callback=[checkpoint_callback, MLflowCallback()]
)

# 학습 완료 후 체크포인트 폴더 전체를 NAS에 업로드
mlflow.log_artifacts("./checkpoints/", artifact_path="checkpoints")

```

## 저장구조 
```
artifacts/
├── checkpoints/
│   ├── rocket_ckpt_10000_steps.zip
│   ├── rocket_ckpt_20000_steps.zip
│   └── rocket_ckpt_30000_steps.zip
└── trained_3d_rocket.zip  ← 최종

```


## commit 

```
# train.py 맨 위에
import subprocess

def check_git_clean():
    dirty = subprocess.check_output(
        ["git", "status", "--porcelain"]
    ).decode().strip()
    
    if dirty:
        print("🚨 커밋 안 된 변경사항이 있어요!")
        print(dirty)
        answer = input("그래도 학습 시작할까요? (y/n): ")
        if answer != "y":
            exit()
    
    commit = subprocess.check_output(
        ["git", "rev-parse", "HEAD"]
    ).decode().strip()
    return commit

def main():
    commit_hash = check_git_clean()  # ← 학습 전 체크
    
    with mlflow.start_run():
        mlflow.set_tag("git_commit", commit_hash)  # ← NAS 기록에 커밋 연결
        # 학습 진행...
```

**위험한 시나리오**
1. 코드 수정 (커밋 안 함)
2. 학습 돌림
3. 가중치 NAS에 저장됨
4. 나중에 "이 가중치 어떤 코드로 만든 거지?" → 모름!
5. 방어코드 추가 !!



# 저장 데이터 흐름
MLflow가 commit hash를 가중치에 태깅해서 나중에 추적할 수 있게

```
[학습 전] ──────────────────────────────
개발자가 코드 수정
    ↓
git commit (수동)
    ↓
python train.py 실행
    ↓
commit hash 자동 캡처 → MLflow에 태깅

[학습 중] ──────────────────────────────
10000스텝마다
    ↓
체크포인트 → NAS 자동 저장
(MLflow run에 commit hash가 붙어있음)

[학습 후] ──────────────────────────────
최종 가중치 → NAS 자동 저장
MLflow 대시보드에서 확인:
    ├── git_commit: a3f9c2b  ← 이 코드로
    ├── lr: 0.001            ← 이 설정으로
    └── artifacts/           ← 이 가중치 나옴

```

# MLflow는 run마다 고유 ID를 자동 생성
- run_name이 같아도 run_id가 다르니까 덮어쓰기 걱정 없음

```
NAS /volume1/docker/mlflow/artifacts/
└── {experiment_id}/
    └── {run_id}/          ← run마다 고유 폴더 자동 생성
        ├── final_model/
        │   └── trained_3d_rocket.zip
        └── checkpoints/
            ├── rocket_ckpt_10000_steps.zip
            └── rocket_ckpt_20000_steps.zip
```



# MLflowCallback : 체크포인트마다 NAS 자동 업로드



