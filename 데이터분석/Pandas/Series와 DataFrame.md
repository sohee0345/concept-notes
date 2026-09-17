---
source:
  - "[[02 정리노트/week04/day16_08.28]]"
---

# Series와 DataFrame

## 1. 개념

Series는 값과 인덱스를 가진 1차원 구조이고 DataFrame은 여러 Series가 컬럼으로 모인 2차원 표 구조이다.

> **핵심:** Pandas 객체는 값뿐 아니라 행 인덱스와 컬럼 이름을 함께 관리한다.

---

## 2. 쉽게 이해하기

Series는 이름표가 붙은 한 줄의 데이터이고 DataFrame은 여러 Series를 옆으로 모은 표이다.

```text
Series 여러 개 → 컬럼으로 결합 → DataFrame
```

---

## 3. 사용 방법

```python
series = pd.Series({"a": 1, "b": 2, "c": 3})
df = pd.DataFrame({"one": [1, 2], "two": [3, 4]})

df.shape
df.index
df.columns
```

- `shape` → 행과 컬럼 개수이다.
- `index` → 각 행을 구분하는 레이블이다.
- `columns` → 컬럼 이름을 담은 Index이다.

---

## 4. 예제

```python
df["new"] = df["one"] + df["two"]
```

기존 컬럼의 원소별 연산 결과를 새 컬럼으로 추가한다.

---

## 5. 헷갈리는 개념 비교

|구분|Series|DataFrame|
|---|---|---|
|차원|1차원|2차원|
|구조|값과 인덱스|여러 컬럼과 행 인덱스|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|Series|인덱스를 가진 1차원 데이터|
|DataFrame|행과 열로 구성된 2차원 데이터|
|Index|행이나 컬럼을 구분하는 레이블|

### 💻 주요 코드

|코드|의미|
|---|---|
|`pd.Series(data)`|Series 생성|
|`pd.DataFrame(data)`|DataFrame 생성|
|`df["new"] = ...`|새 컬럼 생성|

### ⭐ 한 줄 정리

> **Series는 1차원, DataFrame은 여러 Series로 구성된 2차원 표 데이터 구조이다.**

### 🔖 복습할 내용

- [ ] Series와 DataFrame 비교하기
- [ ] index와 columns 확인하기
- [ ] 기존 컬럼으로 새 컬럼 만들기
