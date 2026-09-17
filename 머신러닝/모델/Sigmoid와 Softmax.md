---
source:
  - "[[02 정리노트/week06/day22_09.07]]"
---

# Sigmoid와 Softmax

## 1. 개념

Sigmoid는 실수 하나를 0과 1 사이 값으로 바꾸고 Softmax는 여러 클래스의 로짓을 합이 1인 확률 분포로 바꾼다.

> **핵심:** Sigmoid는 주로 이진 분류, Softmax는 서로 배타적인 다중분류의 확률을 만든다.

---

## 2. 쉽게 이해하기

Sigmoid는 점수 하나를 양성 확률로, Softmax는 여러 점수를 클래스별 확률로 변환한다.

```text
점수 1개 → Sigmoid → 0~1
로짓 여러 개 → Softmax → 합이 1인 확률들
```

---

## 3. 사용 방법

$$\sigma(z)=\frac{1}{1+e^{-z}}$$

```python
def softmax(x):
    shifted = x - np.max(x, axis=-1, keepdims=True)
    exp_x = np.exp(shifted)
    return exp_x / np.sum(exp_x, axis=-1, keepdims=True)
```

최댓값을 먼저 빼면 지수 계산이 지나치게 커지는 것을 막는다.

---

## 4. 예제

다중분류의 `predict_proba()` 결과는 이미 클래스 확률이므로 Softmax를 다시 적용하지 않는다.

---

## 5. 헷갈리는 개념 비교

|구분|Sigmoid|Softmax|
|---|---|---|
|입력|점수 하나|클래스별 로짓|
|출력|0~1 값|합이 1인 확률 분포|
|주요 사용|이진 분류|다중분류|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|로짓|확률 변환 전 모델 점수|
|Sigmoid|점수를 0~1로 변환|
|Softmax|여러 로짓을 확률 분포로 변환|

### 💻 주요 코드

|코드|의미|
|---|---|
|`1 / (1 + np.exp(-x))`|Sigmoid 계산|
|`x - np.max(x)`|Softmax 수치 안정화|

### ⭐ 한 줄 정리

> **Sigmoid와 Softmax는 모델 점수를 이진 또는 다중 클래스 확률로 변환한다.**

### 🔖 복습할 내용

- [ ] 두 함수의 사용 상황 구분하기
- [ ] Softmax 출력 합 설명하기
- [ ] predict_proba에 재적용하지 않기
