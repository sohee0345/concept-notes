# StandardScaler와 MinMaxScaler

## 1. 개념

두 스케일러는 수치형 Feature의 단위와 범위를 변환한다. StandardScaler는 평균과 표준편차를, MinMaxScaler는 최솟값과 최댓값을 기준으로 사용한다.

> **핵심:** 스케일 기준은 train에서만 학습하고 같은 기준으로 test를 변환한다.

------------------------------------------------------------------------

## 2. 비교

| 구분 | StandardScaler | MinMaxScaler |
| --- | --- | --- |
| 기준 | 평균·표준편차 | 최솟값·최댓값 |
| 결과 | 평균 0, 표준편차 1에 맞춤 | 기본적으로 0~1 범위 |

```python
scaler.fit(x_train)
x_train_scaled = scaler.transform(x_train)
x_test_scaled = scaler.transform(x_test)
```

------------------------------------------------------------------------

## 🟦 핵심 정리

### ⭐ 한 줄 정리

> **StandardScaler와 MinMaxScaler는 서로 다른 통계로 수치 범위를 바꾸며 train 기준을 test에 공유한다.**

### 🔖 복습할 내용

- [ ] 두 스케일러의 기준 통계 구분하기
- [ ] train에만 fit하는 이유 설명하기
- [ ] 변환 전후 값 범위 확인하기

