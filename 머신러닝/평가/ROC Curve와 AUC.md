# ROC Curve와 AUC

## 1. 개념

ROC Curve는 여러 임계값에서 FPR과 TPR을 그린 그래프이고 AUC는 그 곡선 아래 면적이다.

$$
TPR=\frac{TP}{TP+FN},\quad
FPR=\frac{FP}{FP+TN}
$$

> **핵심:** AUC는 특정 임계값 하나가 아니라 모델의 양성·음성 순위 구분 능력을 요약한다.

------------------------------------------------------------------------

## 2. 사용 방법

```python
score = model.predict_proba(x_valid)[:, 1]
roc_auc_score(y_valid, score)
RocCurveDisplay.from_predictions(y_valid, score)
```

무작위 수준은 0.5, 완벽한 구분은 1이다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### ⭐ 한 줄 정리

> **ROC는 임계값별 TPR·FPR 관계를 그리고 AUC는 전체 구분 성능을 면적으로 요약한다.**

### 🔖 복습할 내용

- [ ] TPR과 FPR 공식 작성하기
- [ ] ROC 축 설명하기
- [ ] AUC 0.5와 1의 의미 구분하기

