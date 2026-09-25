---
source:
  - "[[02 정리노트/week08/day34_09.23]]"
---

# EfficientNet

## 1. 개념

EfficientNet은 CNN의 깊이, 너비, 입력 이미지 해상도를 함께 조절해 계산량 대비 좋은 성능을 얻도록 설계된 모델 계열이다. B0를 기준 모델로 두고 B1, B2처럼 규모를 키운 변형을 제공한다.

> **핵심:** EfficientNet은 한 가지 축만 크게 만드는 대신 깊이·너비·해상도의 균형을 고려한다.

---

## 2. 쉽게 이해하기

CNN의 성능을 높이기 위해 층만 깊게 하거나 채널만 늘리면 계산량이 커지고 각 요소의 균형이 깨질 수 있다. EfficientNet은 모델이 더 많은 단계에서 특징을 처리하는 정도, 한 단계에서 다루는 채널 수, 입력의 세밀함을 함께 고려한다.

```text
깊이 증가 → 특징 변환 단계 증가
너비 증가 → 각 단계의 채널 증가
해상도 증가 → 더 세밀한 입력 사용
        ↓
세 요소를 함께 조절
```

---

## 3. 사용 방법

```python
from torchvision.models import efficientnet_b0, EfficientNet_B0_Weights

weights = EfficientNet_B0_Weights.DEFAULT
transform = weights.transforms()
model = efficientnet_b0(weights=weights)
```

- `EfficientNet_B0_Weights.DEFAULT` → torchvision이 제공하는 기본 사전학습 가중치다.
- `weights.transforms()` → 해당 가중치에 맞는 크기 조정과 정규화를 반환한다.
- `efficientnet_b0(weights=weights)` → 가중치가 적용된 EfficientNet-B0를 생성한다.

---

## 4. 예제

```python
import torch
from torch import nn
from torchvision.models import efficientnet_b0, EfficientNet_B0_Weights

weights = EfficientNet_B0_Weights.DEFAULT
model = efficientnet_b0(weights=weights)

for param in model.parameters():
    param.requires_grad = False

in_features = model.classifier[1].in_features
model.classifier[1] = nn.Linear(in_features, 3)

images = torch.randn(2, 3, 224, 224)
logits = model(images)
print(logits.shape)
```

출력 형태:

```text
torch.Size([2, 3])
```

기존 특징 추출부를 동결하고 마지막 선형층을 세 클래스 출력으로 교체한다. 실습의 EfficientNet 모델 요약에서도 최종 출력이 `(batch, 3)`인 것을 확인했다. 실제 이미지에는 임의 텐서 대신 반드시 `weights.transforms()`로 만든 변환을 적용해야 한다.

---

## 5. 헷갈리는 개념 비교

| 구분 | EfficientNet | MobileNet |
| --- | --- | --- |
| 주된 목표 | 깊이·너비·해상도의 균형을 통한 효율 향상 | 모바일 환경을 위한 연산량과 모델 크기 절감 |
| 공통점 | 계산 효율을 고려한 CNN | 계산 효율을 고려한 CNN |
| 활용 | 성능과 계산 비용의 균형이 필요한 이미지 작업 | 자원이 제한된 기기에서의 추론 |

둘 다 효율을 중시하지만 설계 목표와 구조가 같지는 않다. 사용 환경의 메모리, 추론 속도, 요구 정확도를 함께 고려해 선택한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| 깊이 | 특징을 변환하는 층의 단계 수 |
| 너비 | 각 층이 처리하는 채널 수 |
| 해상도 | 입력 이미지의 공간적 세밀함 |
| EfficientNet-B0 | EfficientNet 계열의 기준 모델 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `EfficientNet_B0_Weights.DEFAULT` | 기본 사전학습 가중치 선택 |
| `weights.transforms()` | 가중치에 맞는 입력 전처리 생성 |
| `model.classifier[1] = nn.Linear(...)` | 최종 클래스 수에 맞게 출력층 교체 |

### ⭐ 한 줄 정리

> **EfficientNet은 깊이·너비·입력 해상도를 균형 있게 조절해 계산량 대비 성능을 높이는 CNN 계열이다.**

### 🔖 복습할 내용

- [ ] EfficientNet이 함께 고려하는 세 가지 확장 축 설명하기
- [ ] 사전학습 가중치와 `weights.transforms()`를 함께 사용해야 하는 이유 설명하기
- [ ] 새 분류 문제에 맞게 `classifier`를 교체하는 방법 설명하기
