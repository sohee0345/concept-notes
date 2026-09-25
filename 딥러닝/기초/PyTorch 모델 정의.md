---
source:
  - "[[02 정리노트/week07/day28_09.15]]"
---

# PyTorch 모델 정의

## 1. 개념

PyTorch 모델은 `nn.Module`을 상속해 만든다. `__init__()`에서 계층을 등록하고 `forward()`에서 입력이 계층을 통과하는 흐름을 정의하면, PyTorch가 파라미터 관리와 장치 이동, 자동미분을 모델 구조와 연결해 준다.

> **핵심:** 계층은 `__init__()`에 등록하고 데이터의 계산 순서는 `forward()`에 작성한다.

---

## 2. 쉽게 이해하기

`__init__()`이 필요한 부품을 준비하는 설계도라면 `forward()`는 입력이 그 부품들을 어떤 순서로 지나갈지 정한 조립 경로다.

```text
입력 (N, 1, 28, 28)
  ↓ Flatten
(N, 784)
  ↓ Linear + ReLU
(N, 512)
  ↓ Linear
logits (N, 10)
```

---

## 3. 사용 방법

```python
from torch import nn

class Model(nn.Module):
    def __init__(self):
        super().__init__()
        self.flatten = nn.Flatten()
        self.layers = nn.Sequential(
            nn.Linear(28 * 28, 512),
            nn.ReLU(),
            nn.Linear(512, 10),
        )

    def forward(self, x):
        x = self.flatten(x)
        return self.layers(x)
```

- `super().__init__()` → 부모 클래스인 `nn.Module`을 초기화한다.
- `nn.Flatten()` → 배치 차원을 유지하면서 나머지 축을 펼친다.
- `nn.Sequential(...)` → 내부 계층을 지정된 순서대로 실행한다.

---

## 4. 예제

```python
import torch

device = "cuda" if torch.cuda.is_available() else "cpu"
model = Model().to(device)

features = torch.randn(10, 1, 28, 28).to(device)
logits = model(features)

print(logits.shape)
```

실행 결과:

```text
torch.Size([10, 10])
```

이미지 10개가 각각 10개 클래스의 점수를 출력한다. 모델과 입력 텐서는 반드시 같은 장치에 있어야 한다.

---

## 5. 헷갈리는 개념 비교

| 구분 | `nn.Sequential` | `forward()` 직접 연결 |
| --- | --- | --- |
| 흐름 | 계층을 순서대로 실행 | 실행 순서를 코드로 제어 |
| 적합한 구조 | 단순한 직렬 구조 | 분기·재사용·여러 입력이 있는 구조 |
| 장점 | 간결함 | 유연함 |

다중분류에서 마지막 선형 계층의 출력은 logits다. `CrossEntropyLoss`를 사용할 때는 출력층에 ReLU나 Softmax를 넣지 않고 원시 logits를 손실함수에 전달한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

계층의 입출력 크기를 연결하고 모든 파라미터와 입력을 같은 장치에 두는 것이 모델 정의의 기본이다.

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `class Model(nn.Module)` | 사용자 정의 모델 선언 |
| `super().__init__()` | `nn.Module` 초기화 |
| `nn.Sequential(...)` | 계층을 순서대로 묶기 |
| `model.to(device)` | 모델 장치 이동 |

### ⭐ 한 줄 정리

> **PyTorch 모델은 `nn.Module`에 계층을 등록하고 `forward()`로 데이터의 계산 흐름을 정의한다.**

### 🔖 복습할 내용

- [ ] `__init__()`과 `forward()`의 역할 구분하기
- [ ] 인접 계층의 입출력 크기 확인하기
- [ ] 모델과 입력을 같은 장치로 이동하기
