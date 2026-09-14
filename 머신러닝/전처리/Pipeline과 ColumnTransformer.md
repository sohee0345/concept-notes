# Pipeline과 ColumnTransformer

## 1. 개념

`Pipeline`은 전처리와 모델을 순서대로 묶고, `ColumnTransformer`는 수치형·범주형처럼 열 그룹마다 다른 전처리를 적용한다. 두 도구를 함께 사용하면 학습과 예측에서 같은 처리 순서를 재현하고 교차검증 중 데이터 누수를 방지할 수 있다.

> **핵심:** 전처리도 모델 학습의 일부이므로 교차검증의 각 훈련 폴드 안에서 학습해야 한다.

---

## 2. 쉽게 이해하기

```text
원본 데이터
  → 수치형: 결측치 대체 → 스케일링
  → 범주형: 결측치 대체 → 원-핫 인코딩
  → 변환 결과 결합
  → 모델 학습·예측
```

Pipeline은 이 전체 순서를 하나의 모델처럼 다룬다.

---

## 3. 사용 방법

```python
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.linear_model import LogisticRegression

num_pipe = make_pipeline(
    SimpleImputer(strategy="median"),
    StandardScaler(),
)
cat_pipe = make_pipeline(
    SimpleImputer(strategy="most_frequent"),
    OneHotEncoder(handle_unknown="ignore"),
)

preprocessor = ColumnTransformer([
    ("num", num_pipe, numeric_columns),
    ("cat", cat_pipe, categorical_columns),
])

pipeline = make_pipeline(preprocessor, LogisticRegression())
pipeline.fit(X_train, y_train)
```

---

## 4. 하이퍼파라미터 탐색

```python
param_grid = {
    "logisticregression__C": [0.1, 1, 10],
}

search = GridSearchCV(pipeline, param_grid, cv=5)
search.fit(X_train, y_train)
```

파이프라인 내부 파라미터는 `단계이름__파라미터이름`으로 접근한다.

---

## 5. 주의할 점

- 스케일러나 인코더를 전체 데이터에 먼저 `fit()`한 뒤 교차검증하지 않는다.
- 새 범주가 들어올 수 있으면 `OneHotEncoder(handle_unknown="ignore")`를 고려한다.
- 학습된 모델만 저장하지 말고 전처리까지 포함한 파이프라인 전체를 저장한다.
- 단계 이름의 오타는 하이퍼파라미터 탐색 오류로 이어지므로 `get_params().keys()`로 확인할 수 있다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `Pipeline` | 전처리와 모델의 실행 순서를 묶는 구조 |
| `ColumnTransformer` | 열 그룹별로 다른 변환을 적용하는 도구 |
| `__` | 내부 단계의 파라미터에 접근하는 구분자 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `make_pipeline()` | 단계 이름을 자동 생성해 파이프라인 구성 |
| `ColumnTransformer()` | 열별 전처리 정의 |
| `handle_unknown="ignore"` | 학습 때 없던 범주를 오류 없이 처리 |

### ⭐ 한 줄 정리

> **Pipeline과 ColumnTransformer는 열별 전처리와 모델을 하나의 누수 없는 재현 가능한 학습 흐름으로 묶는다.**

### 🔖 복습할 내용

- [ ] 교차검증 전에 전처리를 학습하면 안 되는 이유를 설명할 수 있는가?
- [ ] Pipeline과 ColumnTransformer의 역할을 구분할 수 있는가?
- [ ] 내부 하이퍼파라미터 이름을 지정할 수 있는가?
