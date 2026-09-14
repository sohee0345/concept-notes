# AutoML과 PyCaret

## 1. 개념

AutoML은 데이터 전처리, 알고리즘 비교, 하이퍼파라미터 탐색과 평가 등 반복적인 머신러닝 과정을 자동화하는 방식이다. PyCaret은 분류, 회귀, 군집화 등의 워크플로를 적은 코드로 실행할 수 있게 돕는 AutoML 라이브러리다.

> **핵심:** AutoML은 반복 작업을 줄여 주지만 문제 정의와 결과 검증까지 대신하지는 않는다.

---

## 2. 쉽게 이해하기

여러 모델을 하나씩 직접 만들고 같은 평가 코드를 반복하는 대신, 공통 실험 환경을 먼저 정의한 뒤 모델 비교와 분석을 자동으로 실행한다.

```text
데이터와 타깃 설정
  → 전처리·교차검증 환경 구성
  → 여러 모델 비교
  → 선택 모델 분석·튜닝
  → 새 데이터 예측
  → 파이프라인 저장
```

---

## 3. 사용 방법

```python
from pycaret.classification import (
    setup,
    compare_models,
    predict_model,
    save_model,
)

experiment = setup(
    data=train,
    target="target",
    session_id=42,
    verbose=False,
)

best_model = compare_models(sort="AUC")
predictions = predict_model(best_model, data=test)
save_model(best_model, "classification_pipeline")
```

- `setup()` → 데이터와 타깃, 전처리 및 검증 환경 설정
- `compare_models()` → 여러 알고리즘을 같은 조건에서 비교
- `predict_model()` → 홀드아웃 또는 새 데이터 예측
- `save_model()` → 전처리와 모델이 결합된 파이프라인 저장

---

## 4. 주의할 점

- 자동으로 가장 높은 점수를 낸 모델이 업무 목적에 가장 좋은 모델이라는 뜻은 아니다.
- 데이터 누수, 클래스 불균형, 평가 지표와 테스트 데이터 독립성을 사용자가 확인해야 한다.
- 라이브러리와 주요 의존성 버전에 민감할 수 있으므로 재현 가능한 별도 환경을 관리한다.
- 성능뿐 아니라 추론 시간, 모델 크기, 설명 가능성과 운영 조건도 비교한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `AutoML` | 반복적인 모델 개발 과정을 자동화하는 방식 |
| `Experiment` | 데이터, 전처리와 검증 설정을 묶은 실험 환경 |
| `Pipeline 저장` | 학습된 전처리와 모델을 함께 보존하는 방식 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `setup()` | PyCaret 실험 환경 구성 |
| `compare_models()` | 여러 모델의 교차검증 성능 비교 |
| `predict_model()` | 선택 모델로 예측 |
| `save_model()` | 전체 파이프라인 저장 |

### ⭐ 한 줄 정리

> **PyCaret은 공통 실험 환경에서 여러 모델을 빠르게 비교하지만 최종 판단과 검증은 사용자의 책임이다.**

### 🔖 복습할 내용

- [ ] AutoML이 자동화하는 작업을 설명할 수 있는가?
- [ ] `setup()`과 `compare_models()`의 역할을 구분할 수 있는가?
- [ ] 모델이 아닌 파이프라인 전체를 저장하는 이유를 설명할 수 있는가?
