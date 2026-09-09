# 목표
어떤 코드(commit)로 학습했는지
어떤 하이퍼파라미터로 학습했는지
학습 결과 (reward가 얼마나 나왔는지)


# MLflow 서버로 쓸 때 NAS 요구사항

| 항목 | 최소 | 권장 |
|---|---|---|
| CPU | 1코어 이상 | 2코어 |
| RAM | **1GB** | 2GB |
| 저장공간 | 가중치 용량 + 여유 | SSD 권장 |
| OS | Linux 가능해야 함 | Ubuntu/Debian |
| 네트워크 | 로컬 접근 가능 | 고정 IP |

# 구성
- Nas Backup Server(192.168.1.236) 에 docker 로 설치 
- 192.168.1.236:5050 에 MLFlow Dashboard 접속가능
- docker 내용 

```
version: '3'
services:
  mlflow:
    image: ghcr.io/mlflow/mlflow:v2.11.3
    ports:
      - "5050:5000"
    volumes:
      - /volume1/docker/mlflow/artifacts:/mlflow/artifacts
      - /volume1/docker/mlflow/db:/mlflow/db
    command: >
      mlflow server
      --host 0.0.0.0
      --port 5000
      --backend-store-uri sqlite:////mlflow/db/mlflow.db
      --default-artifact-root /mlflow/artifacts
      --serve-artifacts
    restart: unless-stopped
```


# 사용법 
코드에 추가 하여 프로그램 시작
- 학습 종료시 ? 대시보드에 올라감
 - 에피소드 종료 시 결과? 강제종료는?

──────────────────────────────
개발자가 코드 수정
    ↓
git commit (수동)
    ↓
python train.py 실행
    ↓
학습 진행 (체크포인트 NAS 자동 저장)
    ↓
학습 후 
    ↓
commit hash 자동 캡처 → MLflow에 태깅

    ↓
MLflow 대시보드에서 확인:
    ├── git_commit: a3f9c2b  ← 이 코드로
    ├── lr: 0.001            ← 이 설정으로
    └── artifacts/           ← 이 가중치 나옴

──────────────────────────────



대시 보드에서 비교 
1. missile-rl 실험 클릭
2. 여러 run 체크박스 선택
3. Compare 버튼
4. reward 커브 나란히 비교

