# fit과 transform

## 1. 개념

`fit()`은 데이터에서 전처리 기준을 학습하고 `transform()`은 학습한 기준을 실제 데이터에 적용한다.

> **핵심:** train에는 fit과 transform, test에는 transform만 적용한다.

------------------------------------------------------------------------

## 2. 사용 흐름

```python
scaler.fit(x_train)
x_train_scaled = scaler.transform(x_train)
x_test_scaled = scaler.transform(x_test)
```

`fit_transform(x_train)`은 train에 대한 fit과 transform을 연속해서 수행한다.

------------------------------------------------------------------------

## 3. 주의할 점

- test에 `fit()`하면 평가 정보가 전처리 기준에 들어간다.
- 인코더, 스케일러와 결측치 대체 기준 모두 같은 원칙을 따른다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### ⭐ 한 줄 정리

> **fit으로 train의 기준을 배우고 transform으로 train과 test를 같은 기준에서 변환한다.**

### 🔖 복습할 내용

- [ ] fit과 transform 역할 구분하기
- [ ] fit_transform 사용 위치 설명하기
- [ ] test에 fit하면 안 되는 이유 설명하기

