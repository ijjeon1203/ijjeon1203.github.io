# 미사일 RL 프로젝트 세션 요약

## 프로젝트 구조

```
missile-rl/
├── config.yaml              ← 실험 설정 (이것만 수정)
├── train.py                 ← 학습 실행
├── play.py                  ← 시연 실행
├── rocket_tracking_sim.py   ← 게임 환경 (step() 마지막 줄만 수정)
└── checkpoints/             ← 자동 생성
```

---

## 인프라 구성

```
GitLab        → 코드 버전관리 (config.yaml, train.py, play.py, rocket_tracking_sim.py)
Synology NAS  → MLflow 서버 (Docker) + 가중치 파일 저장
MLflow        → 코드↔가중치 연결 고리 (실험 추적)
```

**MLflow 서버**: `http://192.168.1.236:5050`
**NAS 경로**: `/volume1/docker/mlflow/`
**docker-compose**: `ghcr.io/mlflow/mlflow:v2.11.3` 고정 버전 사용

---

## .gitignore

```gitignore
*.zip
*.pt
checkpoints/
mlruns/
__pycache__/
*.pyc
.venv/
```

---

## config.yaml 최종 구조

```yaml
train:
  algo:          "PPO"
  policy:        "MlpPolicy"
  learning_rate: 0.001
  gamma:         0.99
  activation_fn: "ReLU"
  device:        "cuda"
  num_cpu:       8
  timesteps:     10000

network:
  pi: [128, 128]
  vf: [256, 256]

env:
  boost_time:   5.0
  init_pitch:   30.0
  rocket_speed: 150.0

checkpoint:
  freq:       10000
  save_dir:   "./checkpoints"
  model_name: "trained_3d_rocket"

mlflow:
  tracking_uri: "http://192.168.1.236:5050"
  experiment:   "missile-rl"

play:
  episodes:  20
  use_nas:   false
  run_id:    ""
  artifact:  "final_model/trained_3d_rocket.zip"
```

---

## rocket_tracking_sim.py 수정사항

`step()` 함수 마지막 줄만 교체:

```python
# 기존
return next_state, float(reward), terminated, truncated, {}

# 수정 후
info = {}
if self.mission_result is not None:
    info["mission_status"] = self.mission_result["status"]
return next_state, float(reward), terminated, truncated, info
```

---

## 워크플로우

```
1. config.yaml 수정
2. git add config.yaml
3. git commit -m "실험: lr 변경"
4. python train.py
5. python play.py
```

---

## train.py 핵심 기능

- `config.yaml` 로드 → MLflow 파라미터 자동 기록
- git commit hash 자동 캡처 → MLflow 태깅
- git dirty 상태 경고 (변경 파일 목록 출력)
- `Ctrl+C` 시 긴급 저장 → NAS 자동 업로드
- 체크포인트마다 NAS 자동 업로드
- MLflow 콜백으로 실시간 메트릭 기록:
  - `mean_reward`, `mean_ep_length`
  - `hit_rate`, `loss_of_lock_rate`, `overshoot_rate`, `fallout_rate`
  - `timeout_hit_rate`, `timeout_miss_rate`

---

## play.py 핵심 기능

- `config.yaml`에서 기본값 로드
- 로컬 가중치 또는 NAS에서 다운로드 선택
- `use_nas: true` + `run_id` 설정 시 NAS 자동 다운로드
- 다운로드 시 run_id별 임시폴더에 저장 → 덮어씌워짐 없음

---

## NAS artifacts 구조

```
artifacts/{experiment_id}/{run_id}/
├── config/
│   └── config.yaml
├── final_model/
│   └── trained_3d_rocket.zip
├── checkpoints/
│   ├── rocket_ckpt_10000_steps.zip
│   └── rocket_ckpt_20000_steps.zip
└── emergency/             ← Ctrl+C 시
    └── trained_3d_rocket_emergency.zip
```

---

## zip 파일 생명주기

```
로컬 trained_3d_rocket.zip  → 학습마다 덮어씌워짐 (최신만 유지)
NAS artifacts/{run_id}/     → 모든 실험 영구 보존 (run_id별 폴더)
체크포인트                   → 스텝별로 누적 저장
```

---

## 미완료 사항

- `play.py`에서 `use_nas` config 연동 코드 미완성 (다음 세션에서 이어서)
- `train.py` argparse 완전 제거 확인 필요