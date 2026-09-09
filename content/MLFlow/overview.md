# A.I 모델
AI 모델 = 구조 (코드) + 가중치 (학습 결과물, .pt 파일)
개념적으로는 가중치가 모델의 일부

# lr (Learning Rate, 학습률)
    → AI가 한 번 실수했을 때 얼마나 크게 수정하는지
    → 너무 크면: 왔다갔다 불안정
    → 너무 작으면: 학습이 너무 느림
    → 보통 0.0001 ~ 0.01 사이

# arch (Architecture, 신경망 구조)
    → AI 뇌의 크기/구조
    → pi=[128,128]: 판단하는 뇌 (2층, 각 128개 뉴런)
    → vf=[256,256]: 평가하는 뇌 (2층, 각 256개 뉴런)
    → 크면 더 복잡한 판단 가능, 학습은 느려짐

# reward (보상)
    → AI가 잘했는지 못했는지 점수
    → 미사일이 표적 추적 잘하면 +점수
    → FOV 이탈하면 -점수
    → 이 점수를 최대화하도록 학습


# PyTorch에서 이 둘을 따로 저장하는 이유
```
# 구조만 저장 (코드에 이미 있으니 보통 생략)
# 가중치만 저장 (용량 작고 구조랑 분리 관리)
torch.save(model.state_dict(), "weights.pt")  # 가중치만

# vs 통째로 저장 (구조+가중치 한번에)
torch.save(model, "full_model.pt")  # 전체
```

- torch.save(model, ...)) : 가중치가 모델에 포함된 형태
- 실무에서는 구조 변경 유연성 때문에 가중치만 따로 저장하는 게 관례




# 필요성
# 코드와 가중치 매칭
- 어떤 코드로 만들었는지 확인하기 위해서 필요 
- 모델 구조(hidden layer 크기, layer 수 등)가 가중치 파일이랑 정확히 일치해야 불러올 수 있음
- 코드가 바뀌면 옛날 가중치를 못 씀

구조 변경 유연성 때문에 가중치만 따로 저장하는 게 관례
가중치 파일은 수백MB가 될 수 있어서 git에 올리면 레포가 뚱뚱

# 목표 
ep_50000.pt
    ├── 어떤 코드(commit)로 학습했는지
    ├── 어떤 하이퍼파라미터로 학습했는지
    └── 학습 결과 (reward가 얼마나 나왔는지)
**"코드 + 가중치 매칭 관리"**
"어떤 버전의 모델이 어떻게 학습됐는지 추적


대신 어떤 커밋이 어떤 가중치를 만들었는지는 MLflow나 W&B가 기록


코드        →  Git (GitLab)
가중치(.pt) →  별도 스토리지

```
[게임 환경]  →  state (위치, 속도, 각도 등)  →  [AI 모델 (Policy)]
    ↑                                                      ↓
reward (명중/회피)  ←←←←←←←←  action (방향, 가속 등)

```

# 측정된 데이터 
(state, action, reward, next_state, done)  →  Replay Buffer

# 가중치 파일 (.pt)




# 관리 방법 
온라인 RL (시뮬레이터 기반)에서 "매칭"의 실체
데이터가 실시간 생성되는 구조라 "학습 데이터 파일"이 따로 없어


## 환경 설정 + 결과물을 코드와 묶는 게 핵심

```
소스코드 (git commit)
    ↕
하이퍼파라미터 (lr, gamma, 네트워크 구조 등)
    ↕
환경 설정 (env_id, seed, max_steps 등)
    ↕
학습 결과 (reward curve, 체크포인트)


experiments/
├── exp_001/
│   ├── config.yaml        # 하이퍼파라미터 + 환경설정
│   ├── git_commit.txt     # 실행 시점 commit hash 자동 저장
│   ├── metrics.csv        # reward, loss 등
│   └── checkpoints/
│       └── final.pt
├── exp_002/
│   └── ...



```

규모 작고 혼자 + 온라인 RL이면:

W&B 없이 시작 → 위 구조로 git + yaml + 체크포인트 로컬 관리
실험이 20~30개 넘어가거나 비교가 불편해지면 그때 MLflow UI만 붙이기

지금 당장 W&B/MLflow 설정에 시간 쓰는 것보다 알고리즘 먼저 짜고, 실험 쌓이면서 불편함을 느낄 때 도입하는 게 현실적


# 개요 

## MLflow
- ML 실험 전체 라이프사이클을 관리하는 오픈소스 플랫폼

## 주요 기능
1. MLflow Tracking

학습 실행마다 파라미터, 메트릭, 아티팩트(모델 파일, 그래프 등) 자동 기록
TensorBoard처럼 UI에서 실험 비교 가능

2. MLflow Projects

MLproject 파일로 코드 + 환경(conda, docker)을 패키징
누가 어디서 실행해도 동일한 환경 재현

3. MLflow Models

모델을 표준 포맷으로 저장 → PyTorch, TensorFlow, sklearn 등 다 지원
배포까지 연결 가능

4. MLflow Registry

모델 버전 관리 + Staging/Production 상태 관리



# **가중치 파일 = 학습 결과물**

## 학습 중 체크포인트 저장

```
────────────────────────────────────────
ep_1000.pt   → 아직 못 맞춤 (reward 낮음)
ep_5000.pt   → 조금 배움
ep_10000.pt  → 꽤 잘 맞춤
ep_50000.pt  → 최종 (reward 높음)
```

## 나중에 불러올 때:

```python
model = PolicyNet()  # 구조만 정의
model.load_state_dict(torch.load("ep_50000.pt"))  # 가중치 주입
model.eval()

# 이제 학습 없이 바로 게임 실행 가능
state = env.reset()
action = model(state)  # AI가 바로 판단
```


---

**그래서 "코드와 가중치 매칭"이 왜 중요한가**

```
❌ 위험한 상황
ep_50000.pt  ←  어떤 코드로 만든 거지? PolicyNet 구조가 바뀌었는데?
                → load_state_dict() 에서 shape mismatch 에러!

✅ 안전한 상황
ep_50000.pt  ←  git commit: a3f9c2b (PolicyNet v2, hidden=256)
                → 그 커밋으로 체크아웃하면 항상 로드 가능
```

모델 구조(`hidden layer` 크기, `layer` 수 등)가 가중치 파일이랑 정확히 일치해야 불러올 수 있거든요. 코드가 바뀌면 옛날 가중치를 못 쓰게 돼요.

---

**그래서 지금 하고 싶으신 게 결국 이거죠?**

```
ep_50000.pt
    ├── 어떤 코드(commit)로 학습했는지
    ├── 어떤 하이퍼파라미터로 학습했는지
    └── 학습 결과 (reward가 얼마나 나왔는지)
를 항상 같이 알 수 있게
```

이 구조 바로 잡아드릴게요. 지금 파이썬 게임 프로젝트 폴더 구조가 어떻게 되어 있어요?


# 가중치 파일
- 가중치 파일은 별도 저장소가 필요


# GitLab LFS (Large File Storage)
```
git lfs install
git lfs track "*.pt"   # .pt 파일은 LFS로 관리
git add .gitattributes
git commit -m "track weights with LFS"
```
- .pt 파일도 그냥 git push하면 GitLab에 올라감
- 코드랑 가중치를 같은 레포에서 같은 커밋으로 묶어서 관리할 수 있어서 매칭이 완벽


## 구조
```
git commit a3f9c2b
    ├── policy.py     (코드)
    ├── config.yaml   (하이퍼파라미터)
    └── best.pt       (가중치, LFS에 저장)
```

# gitlab + nas 

**코드와 가중치를 분리 저장하되 연결고리를 만드는 것**
**git commit hash를 폴더명으로 쓰면** 코드↔가중치 매칭 자동

```
GitLab (코드)          로컬 NAS / 외장하드 (가중치)
─────────────          ──────────────────────────
commit: a3f9c2b   →   weights/a3f9c2b/ep_50000.pt
config.yaml            weights/a3f9c2b/best.pt
policy.py
```

## 비교

---

| 방법 | 비용 | 특징 |
|---|---|---|
| **로컬 NAS** | 초기 구매 | 완전 자체 관리, 용량 무제한 |
| **외장하드** | 초기 구매 | 가장 단순, 백업 수동 |
| **Google Drive** | 무료 15GB~ | rclone으로 자동 업로드 가능 |
| **AWS S3 / Cloudflare R2** | 종량제 (R2는 무료티어 넉넉) | MLflow/DVC와 연동 최적 |
| **Hugging Face Hub** | 무료, 대용량 | 모델/가중치 특화 저장소 |

---

**제일 추천하는 조합**

```
GitLab    →  코드 + config.yaml + 실험 메타데이터
HuggingFace Hub  →  가중치 (.pt) 버전 관리, 무료 대용량
MLflow (로컬)    →  실험 결과 추적, commit hash 연결
```

HuggingFace Hub는 모델/가중치 저장 특화라 무료로 대용량 쓸 수 있고, `huggingface_hub` 라이브러리로 업로드/다운로드 자동화도 쉬워요.
