# 정밀도·재현율·F1 Score

## 1. 개념

정밀도는 양성 예측의 정확성을, 재현율은 실제 양성을 찾아낸 비율을 나타낸다. F1은 두 지표의 조화평균이다.

$$
Precision=\frac{TP}{TP+FP},\quad
Recall=\frac{TP}{TP+FN}
$$

$$
F1=2\frac{Precision\cdot Recall}{Precision+Recall}
$$

> **핵심:** FP 비용이 크면 Precision, FN 비용이 크면 Recall을 중요하게 본다.

------------------------------------------------------------------------

## 2. 사용 방법

```python
precision_score(y_true, y_pred)
recall_score(y_true, y_pred)
f1_score(y_true, y_pred)
```

------------------------------------------------------------------------

## 🟦 핵심 정리

### ⭐ 한 줄 정리

> **정밀도와 재현율은 서로 다른 오류 비용을 반영하며 F1은 두 값을 함께 요약한다.**

### 🔖 복습할 내용

- [ ] 세 지표 공식 작성하기
- [ ] FP·FN과 연결하기
- [ ] Accuracy와 차이 설명하기

