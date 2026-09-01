# Matplotlib 기초

## 1. 개념

Matplotlib은 Python의 대표적인 데이터 시각화 라이브러리이다.

그래프를 그릴 때 `Figure`는 전체 도화지, `Axes`는 실제 그래프가 그려지는 좌표 영역이다.

> **핵심:** Figure는 전체 도화지이고 Axes는 실제 그래프를 그리는 영역이다.

---

## 2. 쉽게 이해하기

```text
Figure
┌─────────────────────┐
│  Axes      Axes     │
│  그래프     그래프   │
│                     │
│  Axes      Axes     │
│  그래프     그래프   │
└─────────────────────┘
```

Figure 하나 안에 여러 Axes를 배치할 수 있다.

---

## 3. 사용 방법

```python
import matplotlib.pyplot as plt

plt.figure()
plt.axes()
plt.show()
```

- `plt.figure()` → Figure 생성
- `plt.axes()` → Axes 생성
- `plt.show()` → 그래프 출력

선 그래프:

```python
plt.plot([1, 2, 3, 4])
plt.show()
```

그래프 크기:

```python
plt.figure(figsize=(15, 5))
```

---

## 4. 예제

```python
import numpy as np
import matplotlib.pyplot as plt

plt.figure(figsize=(15, 5))
plt.plot(np.arange(2, 7))
plt.plot(np.arange(5))
plt.show()
```

한 Figure에서 `plt.plot()`을 여러 번 사용하면 여러 선을 함께 표시할 수 있다.

---

## 5. 헷갈리는 개념 비교

| 구분 | Figure | Axes |
|---|---|---|
| 의미 | 전체 도화지 | 실제 그래프 영역 |
| 역할 | 전체 크기·구성 관리 | 그래프 직접 그리기 |
| 비유 | 종이 | 종이 위 좌표 공간 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- Matplotlib → Python 기본 시각화 라이브러리
- Figure → 전체 도화지
- Axes → 실제 그래프가 그려지는 영역
- `figsize` → 그래프 크기

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `plt.figure()` | Figure 생성 |
| `plt.axes()` | Axes 생성 |
| `plt.plot()` | 선 그래프 |
| `plt.show()` | 그래프 출력 |
| `plt.figure(figsize=(15, 5))` | 그래프 크기 지정 |

### ⭐ 한 줄 정리

> **Matplotlib은 Figure 안의 Axes에 그래프를 그리는 구조로 이해하면 쉽다.**

### 🔖 복습할 내용

- [ ] Figure와 Axes 차이
- [ ] `plt.plot()` 역할
- [ ] `figsize=(가로, 세로)` 의미
