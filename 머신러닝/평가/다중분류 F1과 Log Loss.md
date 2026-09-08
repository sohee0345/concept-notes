# 다중분류 F1과 Log Loss

## 1. 개념

다중분류에서는 클래스별 F1 Score를 하나의 값으로 집계하는 기준과 예측 확률 자체를 평가하는 Log Loss를 함께 사용할 수 있다.

---

## 2. F1 평균 방식

| 방식 | 계산 관점 | 특징 |
| --- | --- | --- |
| `micro` | 모든 클래스의 TP·FP·FN을 먼저 합산 | 샘플이 많은 클래스의 영향이 커짐 |
| `macro` | 클래스별 F1을 동일하게 평균 | 소수 클래스도 같은 비중으로 반영 |
| `weighted` | 클래스별 F1을 샘플 수로 가중 평균 | 실제 클래스 분포를 반영 |

```python
from sklearn.metrics import f1_score

micro = f1_score(y_test, y_pred, average="micro")
macro = f1_score(y_test, y_pred, average="macro")
weighted = f1_score(y_test, y_pred, average="weighted")
```

---

## 3. Log Loss

Log Loss는 정답 클래스에 부여한 확률을 평가한다. 정답에 높은 확률을 주면 작아지고, 틀린 클래스에 지나치게 높은 확률을 주면 크게 증가한다.

```python
from sklearn.metrics import log_loss

loss = log_loss(y_test, model.predict_proba(X_test))
```

Log Loss는 작을수록 좋으며, 클래스 이름만 맞았는지 보는 정확도와 달리 모델의 확신 정도까지 반영한다.

---

## 🟦 핵심 정리

### 🎯 한 줄 정리

> F1 평균은 클래스별 성능을 어떤 비중으로 합칠지 정하고, Log Loss는 정답에 부여한 확률의 품질을 평가한다.
