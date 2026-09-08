# Voting과 Stacking

## 1. 개념

Voting과 Stacking은 서로 다른 모델의 예측을 결합하는 앙상블 방법이다. Voting은 정해진 규칙으로 직접 결합하고, Stacking은 기본 모델의 예측을 입력으로 받는 메타 모델을 추가로 학습한다.

---

## 2. Voting

- Hard Voting: 각 모델이 예측한 클래스의 다수결
- Soft Voting: 각 모델의 클래스 확률을 평균한 뒤 가장 큰 값 선택

```python
from sklearn.ensemble import VotingClassifier

voting = VotingClassifier(
    estimators=[("lr", lr), ("rf", rf), ("gb", gb)],
    voting="soft",
)
voting.fit(X_train, y_train)
```

Soft Voting에 참여하는 모델은 `predict_proba()`를 지원해야 하며, 확률 보정 상태가 결과에 영향을 줄 수 있다.

---

## 3. Stacking

```text
원본 특성
  → 여러 기본 모델
  → 각 모델의 검증 폴드 예측
  → 메타 모델
  → 최종 예측
```

메타 모델을 훈련 데이터에 대한 기본 모델의 직접 예측으로 학습하면 누수가 생길 수 있다. 따라서 교차검증의 out-of-fold 예측을 사용한다.

---

## 4. 비교

| 구분 | Voting | Stacking |
| --- | --- | --- |
| 결합 방식 | 다수결 또는 확률 평균 | 메타 모델이 결합 규칙 학습 |
| 복잡도 | 비교적 낮음 | 비교적 높음 |
| 핵심 주의점 | 확률 품질과 모델 다양성 | out-of-fold 예측으로 누수 방지 |

---

## 🟦 핵심 정리

### 🎯 한 줄 정리

> Voting은 예측을 규칙으로 합치고, Stacking은 예측을 다시 학습해 결합한다.
