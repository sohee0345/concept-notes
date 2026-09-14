# Batch·Iteration·Epoch

## 1. 개념

Batch는 한 번의 학습 Step에서 함께 처리하는 샘플 묶음이고, Iteration은 한 Batch로 파라미터를 한 번 갱신하는 과정이다. Epoch는 전체 훈련 데이터를 한 번 모두 사용한 상태를 뜻한다.

$$\text{Iterations per Epoch}=\left\lceil\frac{N}{\text{Batch Size}}\right\rceil$$

> **핵심:** Batch 크기가 100이고 샘플이 60,000개라면 한 Epoch는 600 Iteration이다.

---

## 2. 쉽게 이해하기

```text
전체 학습 데이터 60,000개
  → 100개씩 600개 Batch로 분할
  → Batch마다 1회 파라미터 갱신
  → 600 Iteration 완료 = 1 Epoch
```

---

## 3. 경사하강법 방식

| 방식 | 한 번에 사용하는 샘플 | 특징 |
| --- | --- | --- |
| Batch GD | 전체 데이터 | 안정적이지만 계산 부담이 큼 |
| SGD | 1개 | 빠르고 변동이 큼 |
| Mini-Batch GD | 일부 묶음 | GPU 효율과 안정성의 균형 |

---

## 4. DataLoader 예제

```python
loader = DataLoader(dataset, batch_size=100, shuffle=True)

for epoch in range(10):
    for features, targets in loader:
        prediction = model(features)
        loss = loss_fn(prediction, targets)
```

`len(loader)`는 한 Epoch에 필요한 Batch 수를 반환한다.

---

## 5. 주의할 점

- Batch가 너무 크면 메모리 사용량이 증가한다.
- Batch가 너무 작으면 기울기의 변동이 커질 수 있다.
- 마지막 Batch는 데이터 수가 나누어떨어지지 않으면 더 작을 수 있다.
- Epoch 수가 지나치게 많으면 과적합될 수 있어 검증 손실을 확인한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `Batch` | 한 Step에서 처리하는 샘플 묶음 |
| `Iteration` | Batch 하나로 수행한 파라미터 갱신 1회 |
| `Epoch` | 전체 훈련 데이터를 한 번 모두 사용한 주기 |

### ⭐ 한 줄 정리

> **학습 데이터는 Batch로 나뉘며 각 Batch가 한 Iteration, 전체 Batch를 모두 처리하면 한 Epoch가 된다.**

### 🔖 복습할 내용

- [ ] Batch, Iteration, Epoch를 구분할 수 있는가?
- [ ] 샘플 수와 Batch 크기로 Iteration 수를 계산할 수 있는가?
- [ ] Mini-Batch 학습이 널리 사용되는 이유를 설명할 수 있는가?
