---
source:
  - "[[02 정리노트/week06/day26_09.11]]"
---

# Optimizer

## 1. 개념

Optimizer는 역전파로 계산한 기울기를 이용해 신경망의 가중치와 편향을 갱신하는 알고리즘이다. 기울기를 그대로 사용할 수도 있고 과거 이동 방향이나 최근 기울기 크기를 활용해 파라미터별 이동을 조절할 수도 있다.

> **핵심:** 역전파가 기울기를 계산하면 Optimizer가 그 기울기로 실제 파라미터를 변경한다.

---

## 2. 쉽게 이해하기

기울기가 목적지의 방향을 알려 주는 나침반이라면 Optimizer는 이전 이동 기록과 길의 상태를 참고해 실제 걸음의 방향과 크기를 정하는 방법이다.

```text
손실 → 역전파로 기울기 계산 → Optimizer가 갱신 방법 결정 → 파라미터 변경
```

---

## 3. 사용 방법

```python
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)

optimizer.zero_grad()
loss.backward()
optimizer.step()
```

- SGD → 현재 미니배치의 기울기를 따라 갱신한다.
- Momentum → 이전 이동 방향을 누적해 진동을 줄이고 일관된 방향을 가속한다.
- Adagrad → 파라미터별 누적 기울기로 학습률을 조절하지만 지나치게 작아질 수 있다.
- RMSprop → 최근 제곱 기울기의 이동 평균을 사용한다.
- Adam → Momentum 계열의 1차 모멘트와 RMSprop 계열의 2차 모멘트를 함께 사용한다.

---

## 4. 예제

```python
for x, y in train_loader:
    optimizer.zero_grad()
    prediction = model(x)
    loss = loss_fn(prediction, y)
    loss.backward()
    optimizer.step()
```

PyTorch는 기본적으로 기울기를 누적하므로 매 반복에서 `zero_grad()`로 이전 기울기를 비운 뒤 새 기울기를 계산한다.

---

## 5. 헷갈리는 개념 비교

|구분|SGD|Momentum|Adam|
|---|---|---|---|
|핵심 정보|현재 기울기|현재 기울기와 이전 이동 방향|기울기의 1차·2차 모멘트|
|특징|단순함|진동 완화와 가속|파라미터별 적응적 갱신|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|Optimizer|기울기로 파라미터를 갱신하는 알고리즘|
|Momentum|과거 이동 방향을 누적하는 방법|
|적응적 학습률|파라미터별로 갱신 크기를 조절하는 방식|

### 💻 주요 코드

|코드|의미|
|---|---|
|`optimizer.zero_grad()`|누적 기울기 초기화|
|`loss.backward()`|새 기울기 계산|
|`optimizer.step()`|파라미터 갱신|

### ⭐ 한 줄 정리

> **Optimizer는 역전파가 구한 기울기를 어떤 방향과 크기로 반영할지 결정한다.**

### 🔖 복습할 내용

- [ ] 역전파와 Optimizer의 역할 구분하기
- [ ] SGD·Momentum·Adam의 차이 설명하기
- [ ] `zero_grad()`가 필요한 이유 설명하기
