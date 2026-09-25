---
source:
  - "[[02 정리노트/week08/day34_09.23]]"
---

# Occlusion Attribution

## 1. 개념

Occlusion Attribution은 이미지의 일부 영역을 가린 뒤 목표 클래스의 출력이 얼마나 변하는지 측정하여 영역별 기여도를 추정하는 XAI 방법이다. 모델 내부 구조를 바꾸지 않고 입력을 반복해서 변형하며 설명하기 때문에 동작 방식을 직관적으로 이해할 수 있다.

> **핵심:** 특정 영역을 가렸을 때 예측 점수가 크게 변하면 모델이 그 영역에 민감하게 반응했다고 해석한다.

---

## 2. 쉽게 이해하기

사진 위에 작은 가림판을 놓고 위치를 조금씩 옮기면서 모델의 예측을 반복한다고 생각할 수 있다. 음식을 가렸을 때 피자 점수가 크게 떨어진다면 해당 영역이 피자 예측에 중요한 역할을 했을 가능성이 있다.

```text
원본 이미지의 목표 클래스 점수
  ↓ 영역 하나를 기준값으로 가림
가린 이미지의 목표 클래스 점수
  ↓ 두 점수의 차이 계산
가린 영역의 기여도 추정
```

---

## 3. 사용 방법

```python
from captum.attr import Occlusion

occlusion = Occlusion(model.eval())

attribution = occlusion.attribute(
    input_img,
    strides=(3, 9, 9),
    target=target_index,
    sliding_window_shapes=(3, 20, 20),
    baselines=0,
)
```

- `input_img` → `(배치, 채널, 높이, 너비)` 형태의 모델 입력이다.
- `target` → 기여도를 설명할 목표 클래스 인덱스다.
- `sliding_window_shapes` → 한 번에 가릴 영역의 크기다.
- `strides` → 가림 창을 이동할 간격이다.
- `baselines` → 가린 영역에 채울 기준값이다.

---

## 4. 예제

```python
from captum.attr import Occlusion

model.eval()
occlusion = Occlusion(model)

attribution = occlusion.attribute(
    input_img,
    strides=(3, 9, 9),
    target=0,
    sliding_window_shapes=(3, 20, 20),
    baselines=0,
)

print(attribution.shape)
```

실행 결과:

```text
torch.Size([1, 3, 224, 224])
```

실습에서는 한 장의 RGB 이미지에 대한 기여도가 입력과 같은 형태로 반환되었다. 이를 `(높이, 너비, 채널)` 순서로 변환하여 원본 이미지와 함께 히트맵으로 표시했다.

---

## 5. 헷갈리는 개념 비교

| 구분 | Occlusion Attribution | 일반 예측 확률 |
| --- | --- | --- |
| 목적 | 입력 영역이 목표 클래스에 미친 영향 설명 | 모델이 선택한 클래스의 확신 정도 표시 |
| 계산 | 여러 영역을 가리며 반복 추론 | 원본 입력을 한 번 추론 |
| 결과 | 픽셀 영역별 기여도 | 클래스별 확률 |
| 주의점 | 창 크기·stride·baseline에 따라 달라짐 | 높은 확률이 올바른 근거를 보장하지 않음 |

Occlusion 히트맵은 모델의 민감도를 보여 주지만 현실의 인과관계를 증명하지 않는다. 원본 이미지와 히트맵을 겹칠 때는 모델 입력과 같은 크롭 및 해상도를 사용해야 위치를 올바르게 해석할 수 있다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| 가림 창 | 입력 이미지에서 한 번에 가리는 영역 |
| baseline | 가린 영역을 대체하는 기준값 |
| attribution | 영역이 목표 클래스 출력에 미친 기여도 |
| target | 설명하려는 클래스 인덱스 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `Occlusion(model)` | 모델을 설명할 Occlusion 객체 생성 |
| `occlusion.attribute(...)` | 영역별 기여도 계산 |
| `sliding_window_shapes` | 가림 창의 크기 지정 |
| `strides` | 가림 창의 이동 간격 지정 |

### ⭐ 한 줄 정리

> **Occlusion Attribution은 이미지 일부를 차례로 가렸을 때 목표 클래스 점수가 변하는 정도로 영역별 기여도를 추정한다.**

### 🔖 복습할 내용

- [ ] 가림 영역의 점수 변화가 의미하는 바 설명하기
- [ ] 창 크기와 stride가 해상도·계산량에 미치는 영향 비교하기
- [ ] 히트맵과 원본 이미지의 크롭을 일치시켜야 하는 이유 설명하기

