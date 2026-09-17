---
source:
  - "[[02 정리노트/week06/day25_09.10]]"
---

# AutoML

## 1. 개념

AutoML은 데이터 전처리, 여러 모델의 학습과 비교, 하이퍼파라미터 탐색, 평가처럼 반복되는 머신러닝 절차를 자동화하는 방법이다. 짧은 시간 안에 여러 후보를 같은 기준으로 비교하여 좋은 기준 모델을 찾는 데 유용하다.

---

## 2. 쉽게 이해하기

AutoML은 여러 모델을 한 명씩 시험하는 대신, 정해 둔 평가 기준과 교차검증 방법에 따라 후보 모델을 한꺼번에 시험해 순위를 매기는 도구와 비슷하다. 다만 문제 정의, 올바른 평가 지표 선택, 데이터 누수 확인, 최종 배포 판단까지 대신해 주는 것은 아니다.

```text
데이터 설정 → 전처리 → 모델 비교 → 성능 확인 → 최종 모델 선택·저장
```

---

## 3. 사용 방법

- `setup`에서 데이터, 목표 변수, 전처리 조건, 교차검증 방법 등을 설정한다.
- `compare_models`로 여러 모델을 같은 평가 기준에서 비교한다.
- `plot_model`로 선택한 모델의 성능과 진단 결과를 확인한다.
- `predict_model`로 새로운 데이터에 대한 예측을 만든다.
- 전처리와 모델을 함께 저장해야 학습 때와 같은 변환을 예측 시점에도 재현할 수 있다.

AutoML의 순위만 그대로 채택하지 말고, 사용 목적에 맞는 지표인지와 교차검증 방식이 적절한지를 먼저 확인해야 한다.

---

## 4. 예제

```python
from pycaret.classification import (
    setup, compare_models, plot_model, predict_model,
    save_model, load_model
)

setup(data=train_df, target="target", fold_strategy=cv, session_id=42)
best_model = compare_models(sort="AUC")

plot_model(best_model, plot="auc")
predictions = predict_model(best_model, data=test_df)

save_model(best_model, "best_pipeline")
loaded_model = load_model("best_pipeline")
```

`compare_models(sort="AUC")`는 교차검증 AUC를 기준으로 후보 모델을 비교한다. 저장된 결과에는 예측에 필요한 전처리 과정과 모델이 함께 포함되므로 같은 흐름을 다시 사용할 수 있다.

---

## 5. 헷갈리는 개념 비교

|구분|AutoML|수동 모델링|
|---|---|---|
|장점|여러 후보를 빠르고 일관되게 비교|세부 과정과 탐색 범위를 직접 통제|
|주의점|자동 결과와 설정을 반드시 검토|실험 설계와 반복 작업에 시간이 더 필요|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|AutoML|반복적인 머신러닝 실험 절차를 자동화하는 방법|
|모델 비교|동일한 교차검증과 지표로 여러 후보를 평가하는 과정|
|파이프라인 저장|전처리와 모델을 함께 보존하여 예측 과정을 재현하는 것|

### 💻 주요 코드

|코드|의미|
|---|---|
|`setup(...)`|데이터와 실험 환경 설정|
|`compare_models(sort="AUC")`|AUC 기준 모델 비교|
|`save_model(...)`|전처리를 포함한 모델 파이프라인 저장|

### ⭐ 한 줄 정리

> **AutoML은 반복 실험을 빠르게 자동화하지만, 평가 설계와 결과 해석에 대한 판단까지 대신하지는 않는다.**

### 🔖 복습할 내용

- [ ] AutoML이 자동화하는 단계 설명하기
- [ ] 평가 지표와 교차검증 설정을 직접 확인해야 하는 이유 설명하기
- [ ] 전처리와 모델을 함께 저장해야 하는 이유 설명하기
