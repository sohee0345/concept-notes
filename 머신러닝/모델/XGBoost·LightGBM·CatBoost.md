# XGBoost·LightGBM·CatBoost

## 1. 개념

XGBoost, LightGBM, CatBoost는 Gradient Boosting을 효율적으로 구현하고 규제, 학습 속도, 범주형 특성 처리 등을 강화한 라이브러리다. 어느 모델이 항상 우수한 것은 아니므로 데이터와 평가 기준에 맞춰 비교해야 한다.

---

## 2. 특징 비교

| 모델 | 대표 특징 |
| --- | --- |
| XGBoost | 규제, 결측값 처리, 병렬 계산을 지원하며 일반적으로 균형 있게 트리를 확장 |
| LightGBM | 손실 감소가 큰 리프를 우선 확장하는 leaf-wise 방식과 효율적인 히스토그램 학습 |
| CatBoost | 범주형 특성 처리와 순서 기반 통계, 대칭 트리에 강점 |

LightGBM의 leaf-wise 방식은 빠르게 손실을 줄일 수 있지만 작은 데이터에서는 트리가 깊어져 과적합할 수 있으므로 `num_leaves`, `max_depth`, `min_child_samples` 등을 함께 조절한다.

---

## 3. 사용 방법

```python
from lightgbm import LGBMClassifier

model = LGBMClassifier(
    n_estimators=200,
    learning_rate=0.03,
    max_depth=3,
    random_state=42,
)
model.fit(X_train, y_train)
```

모델과 설정은 계층화 교차검증으로 비교하고, 테스트 데이터는 최종 평가에만 사용한다. 트리 모델은 보통 특성 스케일에 민감하지 않아 표준화가 필수는 아니다.

---

## 4. 주의할 점

- 학습 속도와 성능은 데이터 크기, 특성 형태, 설정과 환경에 따라 달라진다.
- 특성 중요도는 모델의 분할 사용량이나 이득을 나타내며 인과관계를 뜻하지 않는다.
- 범주형 특성을 처리하는 방식이 라이브러리마다 다르므로 입력 형식을 확인한다.

---

## 🟦 핵심 정리

### 🎯 한 줄 정리

> 세 라이브러리는 서로 다른 최적화와 트리 구성 전략을 사용하므로 같은 검증 절차에서 비교해야 한다.
