# Sigmoid와 Softmax

## 1. 개념

Sigmoid와 Softmax는 모델이 출력한 실수 점수인 로짓을 확률처럼 해석할 수 있는 값으로 변환한다. Sigmoid는 각 출력에 독립적으로 적용할 수 있고, Softmax는 여러 클래스가 서로 배타적인 다중분류에서 전체 합을 1로 만든다.

> **핵심:** Sigmoid는 각 출력을 독립적으로 변환하고, Softmax는 여러 출력을 합이 1인 확률 분포로 변환한다.

---

## 2. 사용 방법

```python
import numpy as np

def sigmoid(x):
    return 1 / (1 + np.exp(-x))

def softmax(x):
    x = x - np.max(x, axis=-1, keepdims=True)
    exp_x = np.exp(x)
    return exp_x / exp_x.sum(axis=-1, keepdims=True)
```

- 이진분류의 Sigmoid 출력 하나는 보통 양성 클래스 확률을 뜻한다.
- 다중레이블 분류에서는 레이블별 Sigmoid를 독립적으로 사용할 수 있다.
- 서로 배타적인 다중분류에서는 Softmax를 사용해 클래스 확률의 합을 1로 만든다.

`predict_proba()`가 이미 반환한 확률에는 Softmax를 다시 적용하지 않는다.

---

## 3. 헷갈리는 개념 비교

| 구분 | Sigmoid | Softmax |
| --- | --- | --- |
| 출력 관계 | 각 출력이 독립적 | 출력들이 서로 경쟁 |
| 합 | 반드시 1이 아님 | 전체 합이 1 |
| 대표 용도 | 이진분류, 다중레이블 | 서로 배타적인 다중분류 |

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `로짓` | 확률로 변환하기 전 모델이 출력한 실수 점수 |
| `Sigmoid` | 각 로짓을 독립적인 0과 1 사이의 값으로 변환 |
| `Softmax` | 여러 로짓을 합이 1인 확률 분포로 변환 |

### ⭐ 한 줄 정리

> **Sigmoid는 각 점수를 독립적인 0~1 값으로, Softmax는 여러 점수를 하나의 확률 분포로 변환한다.**

### 🔖 복습할 내용

- [ ] Sigmoid와 Softmax의 출력 관계 비교하기
- [ ] 이진분류·다중레이블·다중분류에 맞는 함수 선택하기
- [ ] `predict_proba()` 결과에 Softmax를 다시 적용하면 안 되는 이유 설명하기
