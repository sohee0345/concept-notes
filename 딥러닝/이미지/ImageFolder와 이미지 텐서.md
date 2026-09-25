---
source:
  - "[[02 정리노트/week07/day27_09.14]]"
---

# ImageFolder와 이미지 텐서

## 1. 개념

`ImageFolder`는 클래스별 폴더에 저장된 이미지를 PyTorch Dataset으로 불러오는 도구다. 하위 폴더 이름을 클래스 이름으로 사용하고 각 클래스에 숫자 라벨을 부여한다. `ToTensor()`를 함께 사용하면 이미지를 `(channel, height, width)` 형태의 텐서로 변환할 수 있다.

> **핵심:** 폴더 구조가 클래스 구성을 결정하고, 변환된 이미지의 축 순서는 `(C, H, W)`가 된다.

---

## 2. 쉽게 이해하기

같은 종류의 이미지를 이름표가 붙은 상자에 나누어 담으면 `ImageFolder`가 상자 이름을 읽어 자동으로 정답 번호를 만든다.

```text
train/pizza/*.jpg → 클래스 pizza → 숫자 라벨
train/steak/*.jpg → 클래스 steak → 숫자 라벨
train/sushi/*.jpg → 클래스 sushi → 숫자 라벨
```

---

## 3. 사용 방법

```python
from torchvision.datasets import ImageFolder
from torchvision.transforms import ToTensor

dataset = ImageFolder(
    root="data/pizza_steak_sushi/train",
    transform=ToTensor(),
)
```

- `root` → 클래스별 하위 폴더가 있는 최상위 경로다.
- `transform` → 이미지를 조회할 때 적용할 변환 규칙이다.
- `dataset[index]` → `(image_tensor, target)`을 반환한다.

---

## 4. 예제

```python
import matplotlib.pyplot as plt
from torch.utils.data import DataLoader

loader = DataLoader(dataset, batch_size=4, shuffle=True)
features, targets = next(iter(loader))

image = features[0].permute(1, 2, 0)
plt.imshow(image)
plt.show()
```

이미지 한 장은 `(C, H, W)`, 배치는 `(N, C, H, W)` 형태다. Matplotlib으로 컬러 이미지를 표시하려면 한 장을 꺼낸 뒤 `permute(1, 2, 0)`으로 `(H, W, C)` 순서로 바꾼다.

---

## 5. 헷갈리는 개념 비교

| 구분 | PyTorch 이미지 텐서 | Matplotlib 컬러 이미지 |
| --- | --- | --- |
| 축 순서 | `(C, H, W)` | `(H, W, C)` |
| 배치 포함 | `(N, C, H, W)` | 한 장씩 표시 |
| 변환 | `ToTensor()` | `permute(1, 2, 0)` |

흑백 이미지는 색상 채널을 제거한 `(H, W)` 형태로도 표시할 수 있다.

---

## 🟦 핵심 정리

### 💡 주요 개념

`ImageFolder`는 폴더 이름과 이미지 파일을 클래스·샘플 관계로 변환하고, `ToTensor()`는 이미지를 PyTorch 연산에 맞는 텐서로 바꾼다.

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `ImageFolder(root=...)` | 폴더 기반 이미지 Dataset 생성 |
| `ToTensor()` | 이미지를 `(C, H, W)` 텐서로 변환 |
| `permute(1, 2, 0)` | 표시를 위해 `(H, W, C)`로 축 변경 |

### ⭐ 한 줄 정리

> **ImageFolder는 클래스별 폴더를 데이터셋으로 만들고, 이미지 텐서는 목적에 맞게 축 순서를 확인해 사용한다.**

### 🔖 복습할 내용

- [ ] ImageFolder가 요구하는 폴더 구조 그리기
- [ ] 이미지 한 장과 배치의 축 설명하기
- [ ] PyTorch 텐서를 Matplotlib 표시 형태로 바꾸기
