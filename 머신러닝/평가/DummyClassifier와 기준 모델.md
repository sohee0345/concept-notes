# DummyClassifier와 기준 모델

## 1. 개념

DummyClassifier는 Feature의 학습 패턴보다 단순한 규칙으로 예측하여 실제 모델 성능을 비교할 기준선을 만든다.

> **핵심:** 복잡한 모델은 최소한 단순 기준 모델보다 의미 있게 좋아야 한다.

------------------------------------------------------------------------

## 2. 최빈 클래스 기준

```python
dummy = DummyClassifier(strategy="most_frequent")
dummy.fit(x_train, y_train)
y_pred = dummy.predict(x_valid)
```

`most_frequent`는 train에서 가장 많은 클래스만 예측한다. 클래스 불균형 데이터에서는 높은 Accuracy가 나올 수 있어 다른 지표도 함께 확인한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### ⭐ 한 줄 정리

> **DummyClassifier는 단순 예측 기준선을 제공해 모델의 실제 개선 정도를 판단하게 한다.**

### 🔖 복습할 내용

- [ ] 기준 모델이 필요한 이유 설명하기
- [ ] most_frequent 전략 설명하기
- [ ] 불균형 데이터의 Accuracy 한계 설명하기

