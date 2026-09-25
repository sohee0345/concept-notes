---
source:
  - "[[02 정리노트/week07/day31_09.18]]"
---

# OpenCV 이미지 처리

## 1. 개념

OpenCV는 이미지와 동영상을 배열 형태로 읽고 크기 변경, 색상 변환, 프레임 추출 등의 처리를 제공하는 라이브러리다. 컬러 이미지를 기본적으로 BGR 채널 순서로 읽는다는 점을 주의해야 한다.

> **핵심:** OpenCV 배열을 다른 시각화 도구와 함께 사용할 때는 채널 순서와 크기 인자 순서를 확인한다.

---

## 2. 쉽게 이해하기

OpenCV와 Matplotlib은 같은 컬러 배열을 서로 다른 채널 순서로 해석한다.

```text
OpenCV: B → G → R
Matplotlib: R → G → B
```

변환 없이 표시하면 빨강과 파랑이 뒤바뀔 수 있다.

---

## 3. 사용 방법

```python
import cv2

image_bgr = cv2.imread("deer.jpg")
image_rgb = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2RGB)
image_gray = cv2.imread("deer.jpg", cv2.IMREAD_GRAYSCALE)
image_resize = cv2.resize(image_bgr, (300, 300))
```

- `cv2.imread()` → 이미지 파일을 배열로 읽는다.
- `cv2.cvtColor()` → 색상 공간이나 채널 순서를 변환한다.
- `cv2.resize()` → `(width, height)` 크기로 변경한다.
- `cv2.VideoCapture()` → 동영상 파일이나 카메라 영상을 연다.

---

## 4. 예제

```python
import cv2
import matplotlib.pyplot as plt

image_bgr = cv2.imread("deer.jpg")
image_rgb = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2RGB)
image_resize = cv2.resize(image_rgb, (300, 300))

plt.imshow(image_resize)
plt.axis("off")
plt.show()
```

실습에서 1200×1200 컬러 이미지를 `(300, 300, 3)` 배열로 축소했다.

---

## 5. 헷갈리는 개념 비교

| 구분 | PIL·Matplotlib | OpenCV |
| --- | --- | --- |
| 컬러 채널 | RGB | 기본 BGR |
| 이미지 크기 표현 | PIL은 `(width, height)` | `resize`는 `(width, height)` |
| 배열 shape | `(height, width, channel)` | `(height, width, channel)` |

함수 인자의 크기 순서와 결과 배열의 shape 순서가 다르므로 가로와 세로를 바꾸어 전달하지 않도록 주의한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

OpenCV는 이미지와 동영상을 NumPy 배열로 처리하며, 다른 라이브러리와 연결할 때 BGR·RGB 차이를 확인해야 한다.

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `cv2.imread(path)` | BGR 컬러 이미지 읽기 |
| `cv2.IMREAD_GRAYSCALE` | 흑백 이미지로 읽기 |
| `cv2.cvtColor(..., cv2.COLOR_BGR2RGB)` | BGR에서 RGB로 변환 |
| `cv2.resize(image, (W, H))` | 이미지 크기 변경 |
| `cv2.VideoCapture(path)` | 동영상 열기 |

### ⭐ 한 줄 정리

> **OpenCV 이미지 처리는 BGR 채널 순서와 `(width, height)` 크기 인자를 정확히 구분하는 것이 중요하다.**

### 🔖 복습할 내용

- [ ] BGR과 RGB 차이 설명하기
- [ ] 배열 shape과 resize 인자 순서 비교하기
- [ ] 동영상에서 특정 프레임 읽는 흐름 설명하기
