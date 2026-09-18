---
source:
  - "[[02 정리노트/week05/day17_08.31]]"
---

# Figure와 Axes

## 1. 개념

Matplotlib의 Figure는 전체 그림 영역이고 Axes는 실제 데이터가 그려지는 좌표 영역이다. 하나의 Figure에는 여러 Axes를 배치할 수 있다.

> **핵심:** Figure가 전체 캔버스이고 Axes가 각 그래프를 그리는 개별 영역이다.

---

## 2. 쉽게 이해하기

Figure를 한 장의 종이, Axes를 종이 안에 나눈 각각의 그래프 칸이라고 생각할 수 있다.

```text
Figure
  ├─ Axes[0,0]
  ├─ Axes[0,1]
  ├─ Axes[1,0]
  └─ Axes[1,1]
```

---

## 3. 사용 방법

```python
fig, axes = plt.subplots(2, 2, figsize=(15, 5))
fig.suptitle("전체 제목")
axes[0, 1].plot(np.arange(2, 7))
axes[0, 1].set_title("그래프 제목")
plt.show()
```

- `figsize` → Figure 크기를 인치 단위로 지정한다.
- `suptitle()` → 전체 제목을 지정한다.
- `set_title()` → 개별 Axes 제목을 지정한다.

---

## 4. 예제

```python
fig, axes = plt.subplots(2, 2, figsize=(15, 5))
fig.suptitle("도화지 제목")

axes[0, 0].plot(np.arange(5))
axes[0, 1].plot(np.arange(2, 7))
axes[1, 0].plot(range(10), np.exp(range(10)))
axes[1, 1].plot(range(1, 1000), np.log1p(range(1, 1000)))

plt.show()
```

`plt.subplots(2, 2)`는 2행 2열의 Axes 네 개를 만들며 `axes[행, 열]`로 원하는 영역을 선택한다.

---

## 5. 헷갈리는 개념 비교

|구분|Figure|Axes|
|---|---|---|
|역할|전체 그림 영역|실제 그래프 좌표 영역|
|제목|`suptitle()`|`set_title()`|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|Figure|전체 시각화 캔버스|
|Axes|데이터가 그려지는 좌표 영역|
|subplot|Figure 안에 배치한 개별 그래프|

### 💻 주요 코드

|코드|의미|
|---|---|
|`plt.subplots(2, 2)`|2×2 Axes 생성|
|`axes[row, col]`|개별 Axes 선택|
|`plt.show()`|완성된 그래프 표시|

### ⭐ 한 줄 정리

> **Matplotlib은 Figure 안에 하나 이상의 Axes를 배치하여 그래프를 구성한다.**

### 🔖 복습할 내용

- [ ] Figure와 Axes의 포함 관계 설명하기
- [ ] 여러 subplot 만들기
- [ ] 전체 제목과 개별 제목 구분하기
