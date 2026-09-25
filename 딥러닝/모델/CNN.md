---
source:
  - "[[02 정리노트/week07/day31_09.18]]"
---

# CNN

## 1. 개념

CNN(Convolutional Neural Network, 합성곱 신경망)은 이미지처럼 공간적인 구조를 가진 데이터를 처리하는 신경망이다. 작은 커널을 이미지 위로 이동시키며 주변 픽셀의 패턴을 찾기 때문에, 이미지를 바로 벡터로 펼치는 완전연결 신경망보다 위치 관계와 지역 특징을 효과적으로 학습할 수 있다.

> **핵심:** CNN은 합성곱으로 지역 특징을 추출하고, 풀링으로 특징 맵을 줄인 뒤 추출된 특징으로 최종 예측을 수행한다.

---

## 2. 쉽게 이해하기

이미지에서 사슴을 구분하려면 특정 픽셀 하나보다 눈, 귀, 뿔을 이루는 주변 픽셀의 모양이 중요하다. CNN의 커널은 작은 돋보기처럼 이미지의 일부 영역을 이동하며 선, 모서리와 질감 같은 패턴을 찾는다.

```text
입력 이미지
  ↓ 합성곱층: 지역 패턴 탐색
특징 맵
  ↓ 활성화 함수: 비선형성 추가
활성화된 특징 맵
  ↓ 풀링층: 크기 축소와 중요 특징 유지
축소된 특징 맵
  ↓ 완전연결층
클래스별 logits
```

앞쪽 합성곱층은 선이나 모서리처럼 단순한 특징을 찾고, 뒤쪽 계층은 이 특징들을 조합해 더 복잡한 형태를 표현한다.

---

## 3. 사용 방법

```python
from torch import nn

feature_extractor = nn.Sequential(
    nn.Conv2d(
        in_channels=3,
        out_channels=16,
        kernel_size=3,
        padding=1,
    ),
    nn.ReLU(),
    nn.MaxPool2d(kernel_size=2),
)
```

- `in_channels` → 입력 이미지의 채널 수다. RGB 이미지는 3, 흑백 이미지는 1이다.
- `out_channels` → 합성곱층이 만들 특징 맵의 수다.
- `kernel_size` → 한 번에 확인할 지역 영역의 크기다.
- `padding` → 이미지 가장자리에 여백을 추가해 출력 크기를 조절한다.
- `stride` → 커널이 한 번에 이동하는 간격이다.
- `MaxPool2d` → 영역 안의 최댓값을 남겨 특징 맵의 높이와 너비를 줄인다.

입력 크기가 $H_{in}\times W_{in}$일 때 합성곱 출력 크기는 다음 식으로 계산할 수 있다.

$$H_{out}=\left\lfloor\frac{H_{in}+2P-D(K-1)-1}{S}+1\right\rfloor$$

$$W_{out}=\left\lfloor\frac{W_{in}+2P-D(K-1)-1}{S}+1\right\rfloor$$

$K$는 커널 크기, $P$는 패딩, $S$는 스트라이드, $D$는 dilation이다.

---

## 4. 예제

```python
import torch
from torch import nn

class CNNClassifier(nn.Module):
    def __init__(self, class_count=3):
        super().__init__()

        self.features = nn.Sequential(
            nn.Conv2d(3, 16, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(kernel_size=2),

            nn.Conv2d(16, 32, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(kernel_size=2),
        )

        self.classifier = nn.Sequential(
            nn.Flatten(),
            nn.Linear(32 * 50 * 50, class_count),
        )

    def forward(self, images):
        features = self.features(images)
        return self.classifier(features)

model = CNNClassifier(class_count=3)
images = torch.randn(10, 3, 200, 200)
logits = model(images)
```

입력 배치는 `day31` 실습의 이미지 형태인 `(10, 3, 200, 200)`을 사용한다. 두 번의 `MaxPool2d(2)`를 거치면 높이와 너비가 `200 → 100 → 50`으로 줄어든다. 마지막 선형 계층은 피자·스테이크·스시 3개 클래스에 대응하는 logits를 출력한다.

---

## 5. 헷갈리는 개념 비교

| 구분 | 완전연결 신경망 | CNN |
| --- | --- | --- |
| 입력 처리 | 이미지를 벡터로 펼침 | 주변 픽셀을 지역 단위로 확인 |
| 공간 관계 | 직접 유지하기 어려움 | 높이·너비 구조를 유지하며 특징 추출 |
| 파라미터 | 모든 입력과 뉴런을 연결 | 같은 커널을 여러 위치에서 공유 |
| 주요 계층 | `Linear` | `Conv2d`, 풀링, `Linear` |

합성곱층과 풀링층은 모두 특징 맵을 처리하지만 역할이 다르다. 합성곱층은 학습 가능한 커널로 특징을 추출하고, 풀링층은 정해진 규칙으로 특징 맵의 크기를 줄인다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| 합성곱 | 커널을 이동시키며 지역적인 패턴을 추출하는 연산 |
| 커널 | 작은 영역의 특징을 찾는 학습 가능한 가중치 |
| 특징 맵 | 합성곱을 통해 추출된 특징의 위치별 반응 |
| 풀링 | 특징 맵 크기를 줄이며 중요한 정보를 남기는 연산 |
| 채널 | 입력 색상 또는 합성곱층이 만든 특징 맵의 축 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `nn.Conv2d(...)` | 2차원 합성곱층 생성 |
| `nn.MaxPool2d(2)` | 높이와 너비를 축소하는 최대 풀링 |
| `nn.Flatten()` | 특징 맵을 분류용 벡터로 변환 |
| `nn.Linear(...)` | 추출된 특징으로 클래스 logits 출력 |

### ⭐ 한 줄 정리

> **CNN은 합성곱 커널로 이미지의 지역 특징을 추출하고 축소·조합하여 최종 클래스를 예측한다.**

### 🔖 복습할 내용

- [ ] 완전연결 신경망과 CNN의 이미지 처리 방식 비교하기
- [ ] `in_channels`와 `out_channels`의 의미 설명하기
- [ ] 커널·패딩·스트라이드로 출력 크기 계산하기
- [ ] 합성곱층과 풀링층의 역할 구분하기
