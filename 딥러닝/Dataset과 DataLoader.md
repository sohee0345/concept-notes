---
source:
  - "[[02 정리노트/week06/day26_09.11]]"
---

# Dataset과 DataLoader

## 1. 개념

Dataset은 개별 샘플과 정답을 제공하는 데이터 모음이고 DataLoader는 Dataset을 배치 단위로 순회하며 필요하면 순서를 섞는 도구이다. 데이터 저장 방식과 학습 반복 방식을 분리하여 같은 Dataset을 다양한 배치 설정으로 사용할 수 있다.

> **핵심:** Dataset이 샘플을 정의하면 DataLoader가 샘플을 배치로 묶어 학습 루프에 공급한다.

---

## 2. 쉽게 이해하기

Dataset이 창고에 저장된 개별 상품이라면 DataLoader는 상품을 정해진 개수만큼 상자에 담아 학습 과정에 전달하는 작업자와 같다.

```text
Dataset의 샘플 → 배치로 묶기·순서 섞기 → DataLoader → 학습 루프
```

---

## 3. 사용 방법

```python
train_loader = DataLoader(
    train_dataset,
    batch_size=100,
    shuffle=True,
)
```

- `batch_size` → 한 번에 가져올 샘플 수를 정한다.
- `shuffle=True` → Epoch마다 학습 샘플의 순서를 섞는다.
- `next(iter(loader))` → 첫 번째 배치를 가져온다.
- 이미지 배치는 일반적으로 `(batch, channel, height, width)` 순서이다.

---

## 4. 예제

```python
train_dataset = datasets.FashionMNIST(
    root="fashion_data",
    train=True,
    download=True,
    transform=ToTensor(),
)

train_loader = DataLoader(train_dataset, batch_size=100, shuffle=True)
images, targets = next(iter(train_loader))
print(images.shape)  # torch.Size([100, 1, 28, 28])
```

FashionMNIST의 한 배치는 이미지 100개, 흑백 채널 1개, 높이와 너비 28인 4차원 Tensor이다. 샘플 60,000개를 배치 크기 100으로 처리하면 한 Epoch에 600개 배치가 필요하다.

---

## 5. 헷갈리는 개념 비교

|구분|Dataset|DataLoader|
|---|---|---|
|역할|개별 샘플과 정답 제공|샘플을 배치로 묶어 순회|
|주요 설정|데이터 위치·변환|배치 크기·셔플 여부|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|Dataset|개별 입력과 정답을 제공하는 객체|
|DataLoader|Dataset을 배치 단위로 순회하는 도구|
|이미지 배치|일반적으로 `(N, C, H, W)` 구조의 Tensor|

### 💻 주요 코드

|코드|의미|
|---|---|
|`DataLoader(dataset, batch_size=100)`|100개씩 배치 구성|
|`shuffle=True`|Epoch마다 순서 섞기|
|`next(iter(loader))`|배치 하나 가져오기|

### ⭐ 한 줄 정리

> **Dataset은 샘플을 정의하고 DataLoader는 샘플을 학습 가능한 배치로 공급한다.**

### 🔖 복습할 내용

- [ ] Dataset과 DataLoader의 역할 구분하기
- [ ] 이미지 배치의 네 축 설명하기
- [ ] 배치 크기로 한 Epoch의 배치 수 계산하기
