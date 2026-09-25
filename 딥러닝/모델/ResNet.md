---
source:
  - "[[02 정리노트/week08/day33_09.22]]"
---

# ResNet

## 1. 개념

ResNet(Residual Network)은 입력을 몇 개의 층 뒤 출력에 직접 더하는 스킵 연결을 사용한 깊은 신경망이다. 합성곱 경로가 학습한 잔차 함수 $F(x)$와 입력 $x$를 더해 $F(x)+x$를 만들기 때문에 정보와 기울기가 깊은 층을 통과하기 쉬워진다.

> **핵심:** ResNet은 입력이 지나가는 지름길을 만들어 깊은 신경망의 학습을 돕는다.

---

## 2. 쉽게 이해하기

일반적인 순차 모델에서는 입력이 모든 층을 차례로 통과해야 한다. 잔차 블록은 합성곱 경로와 shortcut 경로를 함께 두어, 필요한 변화만 $F(x)$로 학습하고 원래 정보는 $x$로 직접 전달할 수 있게 한다.

```text
x ───────────────┐
│                │ shortcut
↓                │
Conv → BN → ReLU │
↓                │
Conv → BN        │
│                │
└──── F(x) + x ──┘
         ↓
       ReLU
```

---

## 3. 사용 방법

```python
from torch import nn

class BasicBlock(nn.Module):
    def __init__(self, in_channels, out_channels, stride=1):
        super().__init__()
        self.residual = nn.Sequential(
            nn.Conv2d(
                in_channels, out_channels,
                kernel_size=3, stride=stride, padding=1,
            ),
            nn.BatchNorm2d(out_channels),
            nn.ReLU(),
            nn.Conv2d(
                out_channels, out_channels,
                kernel_size=3, padding=1,
            ),
            nn.BatchNorm2d(out_channels),
        )

        self.shortcut = nn.Identity()
        if stride != 1 or in_channels != out_channels:
            self.shortcut = nn.Sequential(
                nn.Conv2d(
                    in_channels, out_channels,
                    kernel_size=1, stride=stride,
                ),
                nn.BatchNorm2d(out_channels),
            )

        self.relu = nn.ReLU()

    def forward(self, x):
        return self.relu(self.residual(x) + self.shortcut(x))
```

- `residual` → 두 합성곱으로 $F(x)$를 학습하는 경로다.
- `shortcut` → 입력을 덧셈 위치까지 전달하는 경로다.
- `1×1 Conv2d` → 채널 수나 공간 크기가 다를 때 두 경로의 형태를 맞춘다.

---

## 4. 예제

```python
import torch

block = BasicBlock(in_channels=3, out_channels=64)
images = torch.randn(1, 3, 224, 224)
features = block(images)

print(features.shape)
```

실행 결과:

```text
torch.Size([1, 64, 224, 224])
```

입력과 출력의 채널 수가 다르므로 shortcut 경로의 `1×1` 합성곱이 채널을 3에서 64로 맞춘다. stride는 1이므로 높이와 너비는 유지된다.

---

## 5. 헷갈리는 개념 비교

| 구분 | 일반 순차 블록 | 잔차 블록 |
| --- | --- | --- |
| 정보 흐름 | 모든 층을 차례로 통과 | 합성곱 경로와 shortcut 경로 사용 |
| 출력 | $F(x)$ | $F(x)+x$ |
| 깊은 모델 | 기울기 전달이 어려워질 수 있음 | 직접 경로로 정보와 기울기 전달 보조 |

스킵 연결에서 덧셈은 두 텐서의 형태가 같을 때만 가능하다. 채널 수가 다르거나 stride 2로 공간 크기를 줄이는 블록에서는 shortcut에도 같은 크기 변환이 필요하다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| 잔차 학습 | 전체 변환 대신 입력에서 달라질 부분 $F(x)$를 학습하는 방식 |
| 스킵 연결 | 입력을 여러 층 뒤로 직접 전달하는 경로 |
| BasicBlock | 두 `3×3` 합성곱과 shortcut을 결합한 ResNet 기본 블록 |
| projection shortcut | `1×1` 합성곱으로 덧셈할 텐서의 형태를 맞추는 경로 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `self.residual(x) + self.shortcut(x)` | 두 경로의 결과를 더함 |
| `nn.Identity()` | 형태 변환이 필요 없는 shortcut |
| `nn.Conv2d(..., kernel_size=1)` | shortcut의 채널과 공간 크기 조정 |

### ⭐ 한 줄 정리

> **ResNet은 잔차 함수 $F(x)$에 입력 $x$를 더하는 스킵 연결로 깊은 신경망의 학습을 돕는다.**

### 🔖 복습할 내용

- [ ] $F(x)+x$ 구조가 필요한 이유 설명하기
- [ ] `nn.Identity()`를 사용할 수 있는 조건 설명하기
- [ ] shortcut에 `1×1` 합성곱이 필요한 조건 설명하기
