

# 프로젝트 추천 구조
```
git commit a3f9c2b
    ├── policy.py     (코드)
    ├── config.yaml   (하이퍼파라미터)
    └── best.pt       (가중치, LFS에 저장)

```



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


```
[무엇을 저장하나]          [어디에 저장하나]
─────────────────          ─────────────────
W&B / MLflow               GitLab (코드)
: 실험 메타데이터 추적      NAS (가중치)
: 어떤 코드로?              S3 / HuggingFace
: 어떤 파라미터로?
: 결과가 얼마나?
: 가중치 어디 있는지?

──────────────────────────────────────────────

GitLab   →  코드 버전관리
NAS      →  가중치 파일 백업
MLflow   →  둘을 연결하는 실험 기록부
──────────────────────────────────────────────



NAS        =  실제 파일 보관하는 창고
GitLab     =  코드 보관하는 창고
──────────────────────────────────────────────
MLflow     =  창고 관리 대장
W&B        =  창고 관리 대장 (클라우드 버전)

"a3f9c2b 커밋으로 lr=3e-4 돌린 결과
 reward 95점, 가중치는 NAS/weights/a3f9c2b/에 있음"
→ 이걸 기록하는 게 MLflow/W&B

```



# NAS 폴더 구조

```
/volume1/
└── docker/
    └── mlflow/
        ├── artifacts/    ← 가중치 파일 저장될 곳
        └── db/           ← 실험 기록 DB

```

# 프로젝트 구조 
```
GitLab (코드/설정)         NAS (데이터/결과)
──────────────────         ─────────────────────────────
config.yaml                mlflow/artifacts/
train.py                   └── {experiment_id}/
play.py                        └── {run_id}/
rocket_tracking_sim.py             ├── config/
                                   │   └── config.yaml  ← 참고용 사본
                                   ├── final_model/
                                   │   └── trained_3d_rocket.zip
                                   ├── checkpoints/
                                   │   ├── rocket_ckpt_10000_steps.zip
                                   │   └── rocket_ckpt_20000_steps.zip
                                   └── emergency/  ← Ctrl+C 시
                                       └── trained_3d_rocket_emergency.zip

```


# 재현 

```
python play.py                        → 로컬 가중치 (빠름)
python play.py --run-id abc123...     → NAS 가중치 (다운로드 후 실행)
```
