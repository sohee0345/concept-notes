# PyTorch Tensor와 DataLoader

## 1. 개념

Tensor는 PyTorch의 다차원 데이터 구조로 GPU 연산과 자동미분을 지원한다. DataLoader는 Dataset의 샘플을 배치 단위로 묶고 순서를 섞어 학습 반복문에 공급한다.

> **핵심:** Tensor의 shape·dtype·device를 맞추고 DataLoader로 배치 단위 학습 데이터를 구성한다.

---

## 2. Tensor 사용 방법

```python
import torch

x = torch.tensor([[1, 2], [3, 4]], dtype=torch.float32)

print(x.shape)
print(x.dtype)
print(x.device)
```

```python
x.reshape(1, 4)
x.unsqueeze(0)
x.permute(1, 0)
```

- `reshape()` → 원소 수를 유지하며 shape 변경
- `unsqueeze()` → 크기가 1인 축 추가
- `squeeze()` → 크기가 1인 축 제거
- `permute()` → 축 순서 변경

---

## 3. 결합과 행렬 곱셈

```python
torch.cat((t1, t2), dim=1)
torch.stack((t1, t2), dim=0)
torch.mm(matrix1, matrix2)
torch.bmm(batch1, batch2)
```

`cat()`은 기존 축을 늘리고 `stack()`은 새로운 축을 만든다. `mm()`은 2차원 행렬 곱, `bmm()`은 같은 배치 수를 가진 3차원 텐서의 배치 행렬 곱에 사용한다.

---

## 4. DataLoader 사용 방법

```python
from torch.utils.data import DataLoader

loader = DataLoader(
    dataset,
    batch_size=100,
    shuffle=True,
)

features, targets = next(iter(loader))
```

이미지 배치는 일반적으로 `(batch, channel, height, width)` 형태다. FashionMNIST의 배치 크기가 100이면 shape은 `(100, 1, 28, 28)`이다.

---

## 5. 주의할 점

- 서로 다른 device에 있는 Tensor는 직접 연산할 수 없다.
- `torch.empty()`는 값을 초기화하지 않는다.
- `_`로 끝나는 In-place 연산은 원본을 바꾸며 자동미분에 영향을 줄 수 있다.
- CPU Tensor와 `numpy()` 결과는 메모리를 공유할 수 있어 한쪽 변경이 다른 쪽에 반영될 수 있다.
- 테스트 Dataset을 만들 때는 `train=False`로 지정한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `Tensor` | PyTorch의 다차원 데이터와 연산 단위 |
| `device` | Tensor가 저장되고 연산되는 CPU 또는 GPU |
| `DataLoader` | Dataset을 배치 단위로 공급하는 반복자 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `torch.tensor()` | Tensor 생성 |
| `torch.from_numpy()` | NumPy 배열로부터 Tensor 생성 |
| `DataLoader()` | Dataset의 배치 구성 |

### ⭐ 한 줄 정리

> **PyTorch는 Tensor로 데이터를 계산하고 DataLoader로 Tensor 배치를 반복 학습 과정에 공급한다.**

### 🔖 복습할 내용

- [ ] Tensor의 shape, dtype, device를 설명할 수 있는가?
- [ ] `cat()`과 `stack()`의 차이를 설명할 수 있는가?
- [ ] 이미지 배치의 네 축을 설명할 수 있는가?
