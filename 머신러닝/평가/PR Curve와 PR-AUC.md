# PR Curve와 PR-AUC

## 1. 개념

PR Curve(Precision-Recall Curve)는 분류 임계값을 바꾸면서 Precision과 Recall이 어떻게 달라지는지 그린 곡선이다. PR-AUC는 그 곡선 아래 면적을 요약한 값으로, 희귀한 양성 클래스를 얼마나 정확하고 빠짐없이 찾는지 비교할 때 유용하다.

> **핵심:** PR Curve는 양성 클래스 예측의 정확성과 탐지율 사이의 균형을 보여준다.

---

## 2. 쉽게 이해하기

양성 판정 기준을 낮추면 더 많은 실제 양성을 찾을 수 있어 Recall은 높아지기 쉽지만, 음성을 양성으로 잘못 판단하는 경우도 늘어 Precision이 낮아질 수 있다. 기준을 높이면 반대 현상이 나타난다.

```text
임계값 낮춤
  → 양성 예측 증가
  → Recall 증가 가능
  → Precision 감소 가능
```

무작위 기준선의 Precision은 데이터에서 양성 클래스가 차지하는 비율과 같다. 따라서 양성 비율이 1%라면 기준선도 약 0.01이다.

---

## 3. 사용 방법

```python
from sklearn.metrics import precision_recall_curve, auc

score = model.predict_proba(X_test)[:, 1]
precision, recall, thresholds = precision_recall_curve(y_test, score)
pr_auc = auc(recall, precision)
```

- `predict_proba()[:, 1]` → 양성 클래스의 연속적인 예측 확률
- `precision_recall_curve()` → 임계값별 Precision과 Recall
- `auc(recall, precision)` → PR Curve 아래 면적

> **핵심:** 예측 클래스가 아니라 확률이나 결정 점수를 전달해야 여러 임계값을 평가할 수 있다.

---

## 4. ROC-AUC와 비교

| 구분 | ROC-AUC | PR-AUC |
| --- | --- | --- |
| 축 | FPR과 TPR | Recall과 Precision |
| 초점 | 양성·음성 순위 구분 | 양성 탐지의 정확성과 재현율 |
| 기준 수준 | 보통 0.5 | 양성 클래스 비율에 영향받음 |
| 활용 | 전반적인 구분 능력 비교 | 희귀 양성 탐지가 중요한 문제 |

음성 샘플이 매우 많으면 FPR이 작게 유지되어 ROC-AUC가 좋아 보일 수 있다. 이런 상황에서는 PR Curve가 소수 양성 클래스의 성능 변화를 더 직접적으로 보여준다.

---

## 5. 주의할 점

- PR-AUC 계산 방식과 Average Precision은 비슷하지만 완전히 같은 값이 아닐 수 있으므로 비교할 때 같은 함수를 사용한다.
- 양성 클래스 정의가 바뀌면 Precision, Recall과 PR Curve의 의미도 바뀐다.
- PR-AUC 하나만으로 운영 임계값을 정하지 말고 FP와 FN의 실제 비용을 고려한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `PR Curve` | 임계값별 Precision과 Recall의 관계 |
| `PR-AUC` | PR Curve 아래 면적 |
| `기준선` | 양성 클래스 비율에 해당하는 무작위 수준 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `precision_recall_curve()` | 임계값별 Precision·Recall 계산 |
| `auc(recall, precision)` | PR Curve 면적 계산 |
| `predict_proba()[:, 1]` | 양성 클래스 예측 확률 반환 |

### ⭐ 한 줄 정리

> **PR-AUC는 희귀한 양성 클래스를 정확하고 빠짐없이 찾는 능력을 여러 임계값에 걸쳐 요약한다.**

### 🔖 복습할 내용

- [ ] 임계값과 Precision·Recall의 관계를 설명할 수 있는가?
- [ ] PR Curve의 기준선이 양성 비율과 같은 이유를 설명할 수 있는가?
- [ ] ROC-AUC보다 PR-AUC가 유용한 상황을 설명할 수 있는가?
