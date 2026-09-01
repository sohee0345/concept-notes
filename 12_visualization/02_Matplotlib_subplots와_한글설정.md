# Matplotlib subplots와 한글 설정

## 1. 개념

`subplots()`는 하나의 Figure 안에 여러 개의 Axes를 한 번에 만들 때 사용한다.

Matplotlib에서 한글이 깨지는 경우 `koreanize_matplotlib`을 사용할 수 있다.

> **핵심:** `subplots()`는 한 화면에 여러 그래프를 배치할 때 사용한다.

---

## 2. 쉽게 이해하기

```python
fig, ax = plt.subplots(2, 2)
```

은 다음과 같다.

```text
ax[0,0]    ax[0,1]
ax[1,0]    ax[1,1]
```

즉, 2행 × 2열의 그래프 영역을 만든다.

---

## 3. 사용 방법

```python
fig, ax = plt.subplots(2, 2, figsize=(15, 5))

fig.suptitle("전체 제목")

ax[0, 0].plot([1, 2, 3])
ax[0, 0].set_title("첫 번째 그래프")

plt.show()
```

한글 설정:

```bash
uv add koreanize_matplotlib
```

```python
import koreanize_matplotlib
```

---

## 4. 예제

```python
fig, ax = plt.subplots(2, 2, figsize=(15, 5))

ax[0,0].plot(np.arange(5))
ax[0,1].plot(np.arange(2,7))
ax[1,0].plot(range(10), np.exp(range(10)))
ax[1,1].plot(range(1,1000), np.log1p(range(1,1000)))

plt.show()
```

---

## 5. 헷갈리는 개념 비교

| 구분 | `plt.figure()` | `plt.subplots()` |
|---|---|---|
| 목적 | Figure 생성 | Figure + 여러 Axes 생성 |
| 여러 그래프 | 직접 Axes 추가 필요 | 행·열 구조로 쉽게 생성 |
| 반환값 | Figure 중심 | `fig`, `ax` |

---

## 🟦 핵심 정리

### 💡 주요 개념

- `subplots()` → 여러 그래프 영역 생성
- `ax[row, col]` → 특정 Axes 선택
- `suptitle()` → 전체 Figure 제목
- `set_title()` → 개별 그래프 제목
- `koreanize_matplotlib` → 한글 깨짐 완화

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `plt.subplots(2, 2)` | 2×2 Axes 생성 |
| `ax[0,1]` | 1행 2열 위치 Axes |
| `fig.suptitle()` | 전체 제목 |
| `ax.set_title()` | 개별 제목 |
| `import koreanize_matplotlib` | 한글 설정 |

### ⭐ 한 줄 정리

> **여러 그래프를 한 화면에 배치할 때는 subplots와 ax 인덱싱을 사용한다.**

### 🔖 복습할 내용

- [ ] `ax[row, col]` 인덱싱
- [ ] `suptitle()`과 `set_title()` 차이
- [ ] 한글 깨짐 해결 방법
