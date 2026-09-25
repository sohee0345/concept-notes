---
source:
  - "[[02 정리노트/week07/day27_09.14]]"
---

# 사용자 정의 Dataset

## 1. 개념

사용자 정의 Dataset은 PyTorch가 기본 제공하지 않는 이미지, 표 데이터 등을 일정한 방식으로 조회하기 위해 `torch.utils.data.Dataset`을 상속해 만든 클래스다. 데이터 저장 형식이 달라도 인덱스별 `(feature, target)`을 반환하게 만들면 `DataLoader`와 같은 학습 흐름을 사용할 수 있다.

> **핵심:** 데이터의 위치와 형식에 맞춰 샘플 한 개를 반환하는 규칙을 정의하는 것이 사용자 정의 Dataset의 역할이다.

---

## 2. 쉽게 이해하기

Dataset은 데이터가 어디에 저장되어 있든 번호표를 주면 해당 입력과 정답을 꺼내 주는 창구와 같다.

```text
인덱스 idx
  ↓
__getitem__(idx)
  ↓
(feature, target)
  ↓
DataLoader가 여러 샘플을 배치로 결합
```

---

## 3. 사용 방법

```python
from torch.utils.data import Dataset

class MyDataset(Dataset):
    def __init__(self, data, targets, transform=None):
        self.data = data
        self.targets = targets
        self.transform = transform

    def __len__(self):
        return len(self.data)

    def __getitem__(self, idx):
        feature = self.data[idx]
        target = self.targets[idx]

        if self.transform:
            feature = self.transform(feature)

        return feature, target
```

- `__init__()` → 데이터 경로, 배열, 라벨, 변환 함수처럼 계속 사용할 정보를 저장한다.
- `__len__()` → 데이터셋의 전체 샘플 수를 반환한다.
- `__getitem__(idx)` → 한 인덱스에 해당하는 `feature`와 `target`을 반환한다.

---

## 4. 예제

```python
from PIL import Image
from torch.utils.data import Dataset

class ImageDataset(Dataset):
    def __init__(self, dir_path, transform=None):
        self.path_lst = list(dir_path.glob("*/*.jpg"))
        self.labels = sorted(
            path.name for path in dir_path.iterdir() if path.is_dir()
        )
        self.transform = transform

    def __len__(self):
        return len(self.path_lst)

    def __getitem__(self, idx):
        image_path = self.path_lst[idx]
        feature = Image.open(image_path)
        target = self.labels.index(image_path.parent.stem)

        if self.transform:
            feature = self.transform(feature)

        return feature, target
```

폴더 이름을 정렬해 클래스 목록을 만들면 같은 폴더 구조에서 숫자 라벨의 대응 관계를 일관되게 유지하기 쉽다. 학습용과 테스트용 데이터에는 동일한 클래스 매핑을 적용해야 한다.

---

## 5. 헷갈리는 개념 비교

| 구분 | 기본 제공 Dataset | 사용자 정의 Dataset |
| --- | --- | --- |
| 데이터 | FashionMNIST 등 정해진 형식 | 직접 수집한 이미지·표 데이터 등 |
| 조회 규칙 | 라이브러리에 구현됨 | `__getitem__()`으로 직접 구현 |
| 공통점 | 인덱스별 샘플 제공 | 인덱스별 샘플 제공 |

`Dataset`은 샘플 한 개를 정의하고, `DataLoader`는 여러 샘플을 배치로 묶어 순회한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

사용자 정의 Dataset은 다양한 원본 데이터를 PyTorch가 공통으로 다룰 수 있는 `(feature, target)` 인터페이스로 바꾼다.

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `class MyDataset(Dataset)` | Dataset을 상속해 사용자 데이터셋 정의 |
| `__len__()` | 전체 샘플 수 반환 |
| `__getitem__(idx)` | 인덱스별 입력과 정답 반환 |
| `self.transform(feature)` | 조회 시 입력 데이터 전처리 |

### ⭐ 한 줄 정리

> **사용자 정의 Dataset은 데이터 형식에 맞는 조회 규칙을 구현해 어떤 데이터든 PyTorch 학습 흐름에 연결한다.**

### 🔖 복습할 내용

- [ ] 세 핵심 메서드의 역할 설명하기
- [ ] `feature`와 `target`의 대응 관계 확인하기
- [ ] 학습·테스트 데이터의 라벨 매핑 일치시키기
