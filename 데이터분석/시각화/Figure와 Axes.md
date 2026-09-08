# Figure와 Axes

## 1. 개념

Figure는 Matplotlib 그래프 전체를 담는 그림 영역이고 Axes는 데이터가 실제로 그려지는 좌표 영역이다. 한 Figure에 여러 Axes를 배치할 수 있다.

> **핵심:** Figure 안에 하나 이상의 Axes가 들어간다.

------------------------------------------------------------------------

## 2. 기본 사용법

```python
import matplotlib.pyplot as plt

fig, axes = plt.subplots(2, 2, figsize=(15, 5))
fig.suptitle("전체 제목")

axes[0, 0].plot([1, 2, 3])
axes[0, 0].set_title("개별 제목")

plt.show()
```

- `subplots(2, 2)` → 네 개의 Axes를 만든다.
- `axes[행, 열]` → 배치 위치로 Axes를 선택한다.
- `suptitle()` → Figure 전체 제목을 지정한다.
- `set_title()` → 특정 Axes의 제목을 지정한다.

------------------------------------------------------------------------

## 3. 한글 표시

```bash
uv add koreanize_matplotlib
```

```python
import koreanize_matplotlib
```

패키지를 가져오면 Matplotlib의 한글 글꼴 설정이 적용된다.

------------------------------------------------------------------------

## 🟦 핵심 정리


### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| Figure | 전체 그림 영역이다. |
| Axes | 그래프가 그려지는 좌표 영역이다. |
| subplot | 한 Figure에 배치한 개별 그래프 영역이다. |

### ⭐ 한 줄 정리

> **Figure는 전체 그림을 담고 각 Axes는 독립적인 그래프 좌표 영역을 제공한다.**

### 🔖 복습할 내용

- [ ] Figure와 Axes의 포함 관계 설명하기
- [ ] 2행 2열 subplot 만들기
- [ ] 전체 제목과 개별 제목 설정하기

