---
source:
  - "[[02 정리노트/week06/day26_09.11]]"
---

# PyTorch Tensor

## 1. 개념

Tensor는 PyTorch에서 데이터를 저장하고 연산하는 기본 다차원 배열이다. NumPy 배열과 비슷하지만 CPU와 GPU 사이를 이동할 수 있고 자동미분 계산에 참여할 수 있다.

> **핵심:** Tensor를 사용할 때는 모양, 데이터 타입, 장치를 함께 확인해야 한다.

---

## 2. 쉽게 이해하기

스칼라, 벡터, 행렬과 그보다 높은 차원의 데이터를 하나의 공통 형식으로 다루는 상자이다.

```text
값 + shape + dtype + device → Tensor
```

---

## 3. 사용 방법

```python
x = torch.randn(2, 3, 4)

x.reshape(2, -1)   # (2, 12)
x.permute(0, 2, 1) # (2, 4, 3)
x.unsqueeze(1)     # (2, 1, 3, 4)
```

- `reshape()` → 원소 수를 유지하며 모양을 바꾼다.
- `permute()` → 축의 순서를 바꾼다.
- `unsqueeze()`·`squeeze()` → 크기가 1인 축을 추가하거나 제거한다.
- `cat()` → 기존 축을 따라 이어 붙인다.
- `stack()` → 새로운 축을 만들어 쌓는다.

---

## 4. 예제

```python
a = torch.randn(2, 3)
b = torch.randn(3, 4)
result = torch.mm(a, b)
print(result.shape)  # torch.Size([2, 4])
```

행렬 곱셈에서는 앞 행렬의 마지막 차원과 뒤 행렬의 첫 번째 차원이 같아야 한다. 배치 행렬 곱에는 `torch.bmm()`을 사용하며 배치 차원은 결과에도 유지된다.

---

## 5. 헷갈리는 개념 비교

|구분|`cat()`|`stack()`|
|---|---|---|
|축|기존 축 사용|새 축 생성|
|차원 수|유지|1 증가|

메서드 이름이 `_`로 끝나는 In-place 연산은 원본을 직접 변경한다. CPU Tensor에서 만든 NumPy 배열은 메모리를 공유할 수 있으며, In-place 연산은 자동미분에 필요한 값을 덮어쓸 수 있으므로 주의한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|shape|각 축의 크기|
|dtype|원소의 데이터 타입|
|device|Tensor가 위치한 CPU 또는 GPU|
|In-place 연산|원본 Tensor를 직접 변경하는 연산|

### 💻 주요 코드

|코드|의미|
|---|---|
|`torch.randn(...)`|표준정규분포 값으로 Tensor 생성|
|`reshape(...)`|Tensor 모양 변경|
|`torch.mm(a, b)`|2차원 행렬 곱셈|

### ⭐ 한 줄 정리

> **PyTorch Tensor는 모양·타입·장치 정보를 가지며 GPU 연산과 자동미분을 지원하는 다차원 배열이다.**

### 🔖 복습할 내용

- [ ] shape·dtype·device 설명하기
- [ ] reshape와 permute 차이 설명하기
- [ ] cat과 stack 차이 설명하기
- [ ] In-place 연산의 주의점 설명하기
