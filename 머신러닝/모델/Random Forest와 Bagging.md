# Random Forest와 Bagging

## 1. 개념

Bagging은 여러 부트스트랩 표본에서 모델을 병렬 학습하고 결과를 합쳐 분산을 줄이는 앙상블 방법이다. Random Forest는 결정트리에 Bagging과 무작위 특성 선택을 함께 적용한다.

---

## 2. 동작 방식

```text
훈련 데이터
  → 복원 추출로 여러 표본 생성
  → 각 표본에서 결정트리 학습
  → 분할마다 일부 특성만 후보로 사용
  → 분류는 투표·확률 평균, 회귀는 평균
```

무작위 특성 선택은 트리들이 모두 비슷해지는 것을 막아 앙상블 효과를 높인다.

---

## 3. 사용 방법

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(
    n_estimators=200,
    max_depth=5,
    random_state=42,
    n_jobs=-1,
)
model.fit(X_train, y_train)
```

- `n_estimators`: 트리 수
- `max_depth`: 각 트리의 최대 깊이
- `max_features`: 분할 때 확인할 특성 수
- `min_samples_leaf`: 리프의 최소 샘플 수

---

## 🟦 핵심 정리

### 🎯 한 줄 정리

> Random Forest는 서로 다른 여러 결정트리의 결과를 결합해 단일 트리의 불안정성을 줄인다.
