# ROC Curve와 AUC

## 1. 개념

ROC Curve는 분류 임계값을 바꾸면서 FPR과 TPR이 어떻게 변하는지 나타낸 그래프이다. AUC는 ROC Curve 아래의 면적으로 모델의 클래스 구분 능력을 요약한다.

> **핵심:** ROC Curve는 여러 임계값에서의 성능을 보여주고 AUC는 이를 하나의 값으로 요약한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
예측 확률 또는 Decision Score
  ↓ 여러 임계값 적용
각 임계값의 FPR과 TPR 계산
  ↓
ROC Curve 작성
  ↓
곡선 아래 면적 AUC 계산
```

> **쉽게 말하면:** 합격선을 여러 위치로 옮겨 보면서 정답을 얼마나 잘 구분하는지 전체적으로 확인하는 것이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
from sklearn.metrics import roc_curve, auc

positive_proba = model.predict_proba(x_valid)[:, 1]

fpr, tpr, thresholds = roc_curve(
    y_valid,
    positive_proba,
)
auc_score = auc(fpr, tpr)
```

- `predict_proba()[:, 1]` → Positive 클래스의 예측 확률
- `roc_curve()` → 임계값별 FPR, TPR 계산
- `auc()` → ROC Curve 아래 면적 계산

> **핵심:** `roc_curve()`에는 0·1 예측 클래스가 아니라 확률이나 Decision Score를 전달한다.

------------------------------------------------------------------------

## 4. 예제

$FPR=\frac{FP}{FP+TN}$

$TPR=\frac{TP}{TP+FN}=Recall$

``` text
Dummy AUC: 0.5
Tree AUC:  0.9479604664268065
```

### 결과 해석

- Dummy 모델 AUC `0.5` → 무작위 수준의 구분력
- Decision Tree AUC 약 `0.948` → Dummy 모델보다 높은 구분력

> **결과 해석:** AUC가 클수록 여러 임계값에서 Positive와 Negative를 잘 구분하는 경향이 있다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | ROC Curve | AUC |
| --- | --- | --- |
| 형태 | 그래프 | 하나의 수치 |
| 내용 | 임계값별 FPR·TPR 관계 | ROC Curve 아래 면적 |
| 용도 | 임계값 변화 확인 | 모델 구분력 요약·비교 |

------------------------------------------------------------------------

## 6. 주의할 점

- AUC 구간을 Poor·Good 등으로 나누는 기준은 절대적인 규칙이 아니다.
- AUC가 높아도 실제 서비스에서 사용할 임계값은 업무 비용을 고려해 별도로 정한다.
- Positive 클래스의 확률 또는 Decision Score 열을 올바르게 선택한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `FPR` | 실제 Negative 중 Positive로 잘못 예측한 비율 |
| `TPR` | 실제 Positive 중 찾아낸 비율, Recall |
| `ROC Curve` | 임계값별 FPR과 TPR 관계 |
| `AUC` | ROC Curve 아래 면적 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `predict_proba()[:, 1]` | Positive 예측 확률 선택 |
| `roc_curve()` | FPR·TPR·임계값 계산 |
| `auc()` | 곡선 아래 면적 계산 |

### ⭐ 한 줄 정리

> **ROC Curve는 임계값별 FPR과 TPR의 관계를 보여주고 AUC는 모델의 구분력을 하나의 값으로 요약한다.**

### 🔖 복습할 내용

- [ ] FPR과 TPR 공식 설명하기
- [ ] ROC Curve와 AUC 차이 비교하기
- [ ] AUC 계산에 확률이나 Score가 필요한 이유 설명하기
