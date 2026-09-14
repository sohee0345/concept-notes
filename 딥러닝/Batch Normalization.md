# Batch Normalization

## 1. 개념

Batch Normalization은 학습 중 미니배치의 통계로 층의 활성값을 정규화하고, 학습 가능한 스케일과 이동을 적용하는 기법이다. 깊은 신경망의 학습을 안정시키고 수렴을 빠르게 하는 데 도움을 준다.

> **핵심:** 학습 시 배치 통계를 사용하고 추론 시 누적된 이동 통계를 사용한다.

---

## 2. 동작 방식

미니배치의 평균 $\mu_B$와 분산 $\sigma_B^2$를 사용해 정규화한 뒤, 학습 가능한 $\gamma$와 $\beta$로 다시 크기와 위치를 조절한다.

$$\hat{x}=\frac{x-\mu_B}{\sqrt{\sigma_B^2+\epsilon}}$$

$$y=\gamma\hat{x}+\beta$$

---

## 3. PyTorch 사용 방법

```python
import torch.nn as nn

layer = nn.Sequential(
    nn.Linear(128, 64),
    nn.BatchNorm1d(64),
    nn.ReLU(),
)
```

- `BatchNorm1d` → 벡터나 시계열 특성에 사용
- `BatchNorm2d` → 이미지의 채널별 활성값에 사용
- `model.train()` → 배치 통계를 사용하고 이동 통계를 갱신
- `model.eval()` → 저장된 이동 통계를 사용

---

## 4. 주의할 점

- 추론 전에 `model.eval()`을 호출하지 않으면 예측이 불안정해질 수 있다.
- Batch가 매우 작으면 평균과 분산 추정이 불안정할 수 있다.
- Batch Normalization이 모든 모델 구조에서 필수인 것은 아니다.
- 데이터 입력의 스케일링과 신경망 내부의 Batch Normalization은 적용 위치와 목적이 다르다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `배치 통계` | 현재 미니배치의 평균과 분산 |
| `이동 통계` | 추론에 사용할 누적 평균과 분산 |
| `$\gamma$, $\beta$` | 정규화 후 크기와 위치를 조절하는 학습 파라미터 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `nn.BatchNorm1d()` | 1차원 특성용 Batch Normalization |
| `nn.BatchNorm2d()` | 이미지 채널용 Batch Normalization |
| `model.eval()` | 모델을 추론 모드로 전환 |

### ⭐ 한 줄 정리

> **Batch Normalization은 활성값을 정규화해 학습을 안정시키며 학습과 추론에서 사용하는 통계가 다르다.**

### 🔖 복습할 내용

- [ ] Batch Normalization의 정규화와 재조정 과정을 설명할 수 있는가?
- [ ] 학습 모드와 평가 모드의 통계 사용 차이를 설명할 수 있는가?
- [ ] 입력 스케일링과 Batch Normalization을 구분할 수 있는가?
