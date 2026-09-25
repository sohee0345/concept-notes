---
source:
  - "[[02 정리노트/week07/day29_09.16]]"
---

# PyTorch 학습 루프

## 1. 개념

PyTorch 학습 루프는 모델의 예측과 손실 계산, 기울기 계산, 파라미터 갱신을 반복하는 과정이다. 각 에포크가 끝날 때 평가 루프를 실행하면 학습하지 않은 데이터에 대한 일반화 성능도 함께 확인할 수 있다.

> **핵심:** 학습에서는 파라미터를 갱신하고, 평가에서는 파라미터를 고정한 채 손실과 성능만 측정한다.

---

## 2. 쉽게 이해하기

모델이 문제를 풀고 오답의 원인을 계산한 뒤 답을 고치는 과정을 반복하고, 별도의 시험 문제로 실력을 확인하는 흐름이다.

```text
순전파 → 손실 계산 → 기울기 초기화 → 역전파 → 파라미터 갱신
   ↓
평가 데이터로 손실과 성능 확인
```

---

## 3. 사용 방법

```python
model.train()
prediction = model(X_train)
loss = loss_fn(prediction, y_train)

optimizer.zero_grad()
loss.backward()
optimizer.step()

model.eval()
with torch.inference_mode():
    test_prediction = model(X_test)
    test_loss = loss_fn(test_prediction, y_test)
```

- `model.train()` → 학습 모드로 전환한다.
- `optimizer.zero_grad()` → 이전 반복에서 누적된 기울기를 초기화한다.
- `loss.backward()` → 손실에 대한 파라미터 기울기를 계산한다.
- `optimizer.step()` → 기울기로 파라미터를 갱신한다.
- `model.eval()` → 평가 모드로 전환한다.
- `torch.inference_mode()` → 평가 중 기울기 추적을 비활성화한다.

---

## 4. 예제

```python
epochs = 200
train_losses = []
test_losses = []

for epoch in range(epochs):
    model.train()
    prediction = model(X_train)
    train_loss = loss_fn(prediction, y_train)

    optimizer.zero_grad()
    train_loss.backward()
    optimizer.step()

    model.eval()
    with torch.inference_mode():
        test_prediction = model(X_test)
        test_loss = loss_fn(test_prediction, y_test)

    train_losses.append(train_loss.detach().cpu().item())
    test_losses.append(test_loss.cpu().item())
```

훈련 손실과 테스트 손실을 함께 기록하면 과소적합과 과적합을 판단하는 근거로 사용할 수 있다.

---

## 5. 헷갈리는 개념 비교

| 구분 | 학습 루프 | 평가 루프 |
| --- | --- | --- |
| 모드 | `model.train()` | `model.eval()` |
| 기울기 | 계산함 | `inference_mode()`로 추적하지 않음 |
| 파라미터 갱신 | `optimizer.step()` 실행 | 갱신하지 않음 |
| 목적 | 손실 감소 | 일반화 성능 측정 |

`eval()`은 계층의 동작 모드를 바꾸지만 자체적으로 Autograd를 끄지는 않는다. 평가에서는 `inference_mode()`를 함께 사용한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

에포크마다 학습과 평가를 분리하고 두 손실을 함께 관찰해야 모델의 학습 상태를 올바르게 판단할 수 있다.

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `model.train()` | 학습 모드 전환 |
| `optimizer.zero_grad()` | 누적 기울기 초기화 |
| `loss.backward()` | 기울기 계산 |
| `optimizer.step()` | 파라미터 갱신 |
| `torch.inference_mode()` | 평가 연산의 기울기 추적 중단 |

### ⭐ 한 줄 정리

> **PyTorch 학습 루프는 손실의 기울기로 파라미터를 반복 갱신하고 별도의 평가 루프로 일반화 성능을 확인한다.**

### 🔖 복습할 내용

- [ ] 학습 단계의 실행 순서 외우기
- [ ] 학습 모드와 평가 모드 구분하기
- [ ] 훈련·테스트 손실 곡선 해석하기
