
# 모델 불러오기 

```
model = PolicyNet()  # 구조만 정의
model.load_state_dict(torch.load("ep_50000.pt"))  # 가중치 주입
model.eval()

# 이제 학습 없이 바로 게임 실행 가능
state = env.reset()
action = model(state)  # AI가 바로 판단

```
