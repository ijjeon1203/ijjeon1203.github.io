# 종류 
**1. Weights & Biases (W&B)** ← 현재 RL 연구자들 사이에서 가장 인기
- 설치 없이 클라우드에 바로 기록, UI가 MLflow보다 훨씬 세련됨
- RL 특화 기능이 잘 되어 있음 (reward curve, video 기록 등)
- 무료 플랜으로도 개인 프로젝트 충분
- 단점: 클라우드 기반 → 인터넷 필요, 데이터가 W&B 서버로 올라감

**2. DVC (Data Version Control)**
- Git에 붙여 쓰는 데이터/모델 버전관리 특화
- 코드는 git, 데이터/모델은 DVC로 → 완전한 재현성
- MLflow처럼 실험 메트릭 비교 UI는 약함
- 단점: 설정이 다소 복잡

**3. Neptune.ai**
- W&B랑 비슷한 포지션, UI 좋음
- 팀 협업에 강점, 개인은 W&B 대비 장점이 적음

**4. Comet ML**
- W&B/Neptune과 유사, 셋 중에 가장 덜 쓰임

---

**현실적인 추천**

| 상황 | 추천 |
|---|---|
| 혼자, 로컬 완결, 데이터 외부 유출 NO | **MLflow** |
| 혼자, 빠르게 시작, UI 좋아야 함 | **W&B** |
| 코드+데이터 재현성이 최우선 | **DVC + MLflow** 조합 |
| 논문 쓰거나 공개 프로젝트 | **W&B** (링크 공유 편함) |

순수 PyTorch 직접 구현 + 강화학습이면 **W&B**가 가장 빠르게 붙이기 쉽고 RL 커뮤니티에서 가장 많이 씁니다.

 `wandb.log({"reward": r})` 한 줄이면 바로 클라우드 대시보드에 찍혀요.

데이터를 외부에 올리기 싫으시면 MLflow 로컬


GitLab 연동 기준으로 보면 선택지가 꽤 좁혀져요.

**GitLab과 연동이 되는 것들**

| 도구 | GitLab 연동 방식 | 난이도 |
|---|---|---|
| **MLflow** | GitLab CI/CD에서 `mlflow run` 실행, commit hash 수동 태깅 | 중간 |
| **W&B** | GitLab CI 파이프라인에 wandb 환경변수만 추가하면 자동 연동 | **쉬움** |
| **DVC** | GitLab을 remote storage로 직접 사용 가능 (DVC for GitLab) | 중간 |
| **Neptune** | CI 연동 가능하지만 GitLab 특화 기능 없음 | 중간 |

---

**처음이고 규모 작으면 이렇게 생각하시면 돼요**

W&B가 가장 무난한 이유:

- `pip install wandb` → `wandb login` → 코드에 5줄 추가면 끝
- GitLab에서는 CI 변수에 `WANDB_API_KEY`만 등록하면 파이프라인 실행 결과가 자동으로 W&B 대시보드에 연결됨
- git commit hash를 **자동으로** 캡처해줌 (직접 태깅 불필요)
- 나중에 규모 커져도 그대로 쓸 수 있음

```python
# 이게 전부예요
import wandb

wandb.init(project="my-rl-project")
wandb.config.update({"lr": 3e-4, "gamma": 0.99})

# 학습 루프 안에서
wandb.log({"reward": episode_reward, "loss": loss}, step=episode)

# 끝
wandb.finish()
```

GitLab CI 설정도 이게 전부고요:

```yaml
# .gitlab-ci.yml
train:
  script:
    - pip install wandb torch
    - python train.py
  variables:
    WANDB_API_KEY: $WANDB_API_KEY  # GitLab CI 변수에 등록
```

---

**결론**

처음 시작 + 규모 작음 + GitLab 연동 → **W&B** 추천합니다. 나중에 로컬 완결이 필요해지거나 데이터 보안 이슈가 생기면 그때 MLflow로 마이그레이션해도 늦지 않아요. 진입장벽이 가장 낮고 RL 예제도 많아서 레퍼런스 찾기도 편합니다.

W&B로 시작하는 방향으로 세팅 도와드릴까요?




# 추천 구조

```
missile-rl/
├── game/                    # 파이썬 게임 환경
│   ├── env.py               # Gym 형태로 래핑
│   ├── missile.py
│   └── renderer.py
│
├── model/                   # 모델 구조 정의
│   ├── policy.py            # PolicyNet 클래스
│   └── weights/             # 가중치 파일들
│       ├── ep_1000.pt
│       ├── ep_5000.pt
│       └── best.pt
│
├── train.py                 # 학습 실행
├── play.py                  # 가중치 불러와서 게임 실행
├── config.yaml              # 하이퍼파라미터
└── experiments/             # 실험 결과 기록
```

---

**weights/ 는 .gitignore 처리**

가중치 파일은 수백MB가 될 수 있어서 git에 올리면 레포가 뚱뚱해져요.

```
# .gitignore
model/weights/*.pt
experiments/
```

대신 **어떤 커밋이 어떤 가중치를 만들었는지**는 MLflow나 W&B가 기록해줘요.

---

# **그럼 MLflow vs W&B 선택**

| | MLflow | W&B |
|---|---|---|
| 가중치 저장 | 로컬 (`mlruns/`) | 클라우드 |
| GitLab 연동 | 수동 commit hash 태깅 | 자동 |
| 설정 난이도 | 중간 | 쉬움 |
| 혼자 + 로컬 완결 | ✅ 적합 | 클라우드 의존 |

GitLab 쓰신다고 하셨으니 **W&B**가 편하긴 한데, 가중치를 클라우드에 올리기 싫으면 **MLflow 로컬**이 맞아요.
