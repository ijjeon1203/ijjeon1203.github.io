# artifacts 




```
현재 저장 예정 ✅
├── lr
├── gamma
├── arch (pi, vf)
├── timesteps
├── num_cpu
└── 가중치 (.zip)

추가하면 좋은 것들 📋
├── 환경 파라미터
│   ├── boost_time (5.0)
│   ├── init_pitch (30.0)
│   └── rocket_speed (150.0)
│
├── 학습 결과 메트릭
│   ├── mean_reward (평균 보상)
│   ├── mean_ep_length (평균 에피소드 길이)
│   ├── hit_rate (명중률)
│   ├── loss_of_lock_rate (FOV 이탈률)
│   ├── overshoot_rate (오버슈트률)
│   └── fallout_rate (추락률)
│
├── 학습 환경 정보
│   ├── git_commit
│   ├── 학습 시작/종료 시간
│   └── 총 학습 소요 시간
│
└── 기타
    ├── activation_fn (ReLU)
    └── device (cuda/cpu)
```



| 항목 | 설명 |
|---|---|
| `mean_reward` | 학습이 잘 되고 있는지 |
| `hit_rate` | 명중률 추이 |
| `fallout_rate` | 추락률 (초반에 높음) |
| `loss_of_lock_rate` | FOV 이탈률 |
| `demo_hit_rate` | 최종 시연 명중률 |
| `git_commit` | 어떤 코드로 학습했는지 |


# artifacts
```
trained_3d_rocket.zip
├── policy.pth            ← 실제 신경망 가중치 (핵심!)
├── policy.optimizer.pth  ← 옵티마이저 상태
└── data                  ← 모델 메타데이터 (JSON)

```

# policy.pth            ← 실제 신경망 가중치 (핵심!)
신경망의 모든 뉴런 가중치값
→ AI가 "학습한 것" 그 자체
→ 이것만 있으면 추론(시연) 가능
→ PyTorch의 state_dict 형식

# policy.optimizer.pth  ← 옵티마이저 상태
Adam/SGD 옵티마이저의 내부 상태
→ 학습 모멘텀, 그래디언트 이력 등
→ 이어학습(resume)할 때 필요
→ 시연만 할 때는 불필요

# data                  ← 모델 메타데이터 (JSON)
모델 구조 메타데이터
→ observation_space, action_space
→ 하이퍼파라미터
→ SB3 버전 정보
→ PPO.load() 할 때 이걸 먼저 읽어서 구조 복원


# code 
```
# 시연만 할 때 (policy.pth만 필요)
model = PPO.load("trained_3d_rocket", device="cpu")
model.predict(obs)  # 추론만

# 이어학습할 때 (policy.pth + policy.optimizer.pth 둘 다 필요)
model = PPO.load("trained_3d_rocket", env=env, device="cuda")
model.learn(total_timesteps=10000)  # 학습 재개

```

# zip 파일 생명 주기 
```
[학습 시작]
    ↓
trained_3d_rocket.zip 있으면? → 이어학습
없으면?                        → 새로 학습
    ↓
[학습 중 - 10000스텝마다]
    ↓
checkpoints/rocket_ckpt_10000_steps.zip  생성 (로컬)
    ↓ 자동 업로드
NAS artifacts/{run_id}/checkpoints/rocket_ckpt_10000_steps.zip
    ↓
[학습 완료]
    ↓
trained_3d_rocket.zip  생성/덮어씌움 (로컬)
    ↓ 자동 업로드
NAS artifacts/{run_id}/final_model/trained_3d_rocket.zip
```

# play.py에서 Nas로 받아 올때 
```
NAS artifacts/{run_id}/final_model/trained_3d_rocket.zip
    ↓ download_artifacts()
로컬 임시폴더/trained_3d_rocket.zip  ← 임시 다운로드
    ↓ PPO.load()
메모리에 올라감
    ↓
시연 실행
```

download_artifacts()는 run_id별로 다른 경로에 저장

PPO.load() 할 때 파일명