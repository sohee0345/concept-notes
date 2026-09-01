# CSV · DataFrame · dtype

## 1. 개념

CSV 파일을 pandas로 불러오면 행(row)과 열(column)로 구성된 2차원 `DataFrame`으로 다룰 수 있다.

`df.info()`를 통해 전체 행 개수인 `RangeIndex`와 각 컬럼의 `dtype`을 확인할 수 있다.

> **핵심:** CSV를 불러온 뒤에는 DataFrame의 행 개수와 dtype이 의도한 형태인지 확인해야 한다.

---

## 2. 쉽게 이해하기

```text
        column
          ↓
      이름  나이  지역
row → 길동  20   서울
```

숫자처럼 보여도 계산용 숫자가 아니라 코드값이라면 문자열로 읽어야 할 수 있다.

---

## 3. 사용 방법

```python
import pandas as pd

df = pd.read_csv(
    "data.csv",
    encoding="utf-8",
    dtype={"시점": "object"}
)

df.info()
```

---

## 4. 예제

```text
RangeIndex: 100 entries, 0 to 99
```

→ 행이 총 100개 있다는 의미다.

```python
dtype={"시점": "object"}
```

→ `시점` 컬럼을 문자열처럼 처리한다.

---

## 5. 헷갈리는 개념 비교

| 구분 | 의미 |
|---|---|
| Row | 데이터 한 건 |
| Column | 변수/항목 |
| RangeIndex | 행 범위와 개수 |
| dtype | 컬럼 데이터 타입 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- `DataFrame` → 2차원 데이터
- `RangeIndex` → 행 개수 확인
- `dtype` → 컬럼 타입
- `object` → 문자열 형태 처리

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `pd.read_csv()` | CSV 불러오기 |
| `df.info()` | 행 개수·dtype 확인 |
| `dtype={'컬럼':'object'}` | 특정 컬럼 문자열 처리 |

### ⭐ 한 줄 정리

> **CSV를 불러온 뒤에는 DataFrame의 행 개수와 dtype이 의도한 형태인지 확인해야 한다.**

### 🔖 복습할 내용

- [ ] Row와 Column 차이
- [ ] `RangeIndex` 읽는 법
- [ ] 코드성 숫자를 문자열로 처리하는 이유
