# Boosting과 Gradient Boosting

## 1. 개념

Boosting은 약한 학습기를 순차적으로 추가하면서 앞선 모델이 부족했던 부분을 보완하는 앙상블 방법이다. Gradient Boosting은 손실 함수가 줄어드는 방향, 즉 음의 그래디언트를 다음 모델이 학습하도록 구성한다.

---

## 2. 동작 방식

```text
첫 번째 약한 모델 학습
  → 현재 예측의 오차 계산
  → 오차를 줄이는 다음 모델 학습
  → 학습률만큼 결과 추가
  → 정해진 횟수만큼 반복
```

`learning_rate`를 낮추면 각 트리의 기여가 작아지므로 보통 더 많은 `n_estimators`가 필요하다. 깊은 트리와 많은 반복은 표현력을 높이지만 과적합 위험과 계산량도 증가시킨다.

---

## 3. 사용 방법

```python
from sklearn.ensemble import GradientBoostingClassifier

model = GradientBoostingClassifier(
    n_estimators=100,
    learning_rate=0.1,
    max_depth=2,
    random_state=42,
)
model.fit(X_train, y_train)
```

---

## 🟦 핵심 정리

### 🎯 한 줄 정리

> Gradient Boosting은 이전 예측의 손실을 줄이는 트리를 순차적으로 더해 강한 모델을 만든다.
