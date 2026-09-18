---
source:
  - "[[02 정리노트/week05/day21_09.04]]"
---

# ROC와 AUC

## 1. 개념

ROC Curve는 여러 임계값에서 FPR과 TPR의 관계를 그린 곡선이고 AUC는 그 아래 면적이다. AUC는 모델이 양성과 음성을 구분해 순위를 매기는 능력을 요약한다.

> **핵심:** ROC AUC는 특정 임계값 하나를 정하기 전 전체 임계값 범위의 구분 능력을 평가한다.

---

## 2. 쉽게 이해하기

임계값을 계속 바꾸며 실제 양성을 얼마나 찾고 실제 음성을 얼마나 잘못 양성으로 판단하는지 기록한 그래프이다.

```text
여러 임계값 → TPR·FPR 계산 → ROC Curve → 면적 AUC
```

---

## 3. 사용 방법

$$
\mathrm{TPR}=\frac{TP}{TP+FN},\qquad
\mathrm{FPR}=\frac{FP}{FP+TN}
$$

```python
auc_score = roc_auc_score(y_valid, probability)
RocCurveDisplay.from_predictions(y_valid, probability)
```

---

## 4. 예제

```python
from sklearn.metrics import auc, roc_curve

fpr, tpr, thresholds = roc_curve(y_valid, pred_tree)
roc_auc = auc(fpr, tpr)

print(f"model: {roc_auc}")
```

AUC `0.5`는 무작위 순위 수준이고 `1`은 완벽한 구분이다. 성능 등급을 나누는 고정 구간은 분야에 따라 달라질 수 있다.

---

## 5. 헷갈리는 개념 비교

|구분|ROC Curve|AUC|
|---|---|---|
|표현|임계값별 FPR·TPR 관계|ROC 아래 면적 하나의 값|
|목적|Trade-off 확인|구분 순위 능력 요약|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|TPR|실제 양성 중 찾아낸 비율|
|FPR|실제 음성 중 양성으로 잘못 예측한 비율|
|AUC|ROC Curve 아래 면적|

### 💻 주요 코드

|코드|의미|
|---|---|
|`roc_auc_score()`|AUC 계산|
|`RocCurveDisplay.from_predictions()`|ROC Curve 표시|

### ⭐ 한 줄 정리

> **ROC와 AUC는 여러 임계값에서 모델의 양성·음성 구분 능력을 평가한다.**

### 🔖 복습할 내용

- [ ] TPR과 FPR 계산하기
- [ ] ROC Curve 축 설명하기
- [ ] AUC 0.5와 1 해석하기
