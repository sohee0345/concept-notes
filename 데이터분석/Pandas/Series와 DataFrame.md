# Series와 DataFrame

## 1. 개념

`Series`는 Pandas의 1차원 데이터 구조이고, `DataFrame`은 여러 Series가 모인 2차원 표 구조이다. 둘 다 데이터 값과 이를 구분하는 인덱스를 가진다.

> **핵심:** Series는 한 컬럼인 벡터처럼, DataFrame은 행과 열을 가진 행렬처럼 이해한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
Series
  → 한 줄의 데이터
  → 1차원, 한 컬럼

DataFrame
  → 여러 Series가 나란히 모인 표
  → 2차원, 여러 컬럼
```

> **쉽게 말하면:** Series는 표의 한 열이고 DataFrame은 여러 열을 합친 전체 표이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
import numpy as np
import pandas as pd

s = pd.Series(
    data={"a": 1, "b": 2, "c": 3},
    dtype=np.int16,
)

df = pd.DataFrame({
    "one": pd.Series(np.random.randn(5)),
    "two": pd.Series(np.random.randn(5)),
})
```

- `data` → 저장할 값
- `dtype` → 값의 자료형
- `index` → 각 행을 구분하는 값
- `columns` → DataFrame의 컬럼 이름
- `shape` → `(행 개수, 열 개수)`

> **핵심:** `index`, `columns`, `shape`, `info()`로 데이터 구조를 먼저 확인한다.

------------------------------------------------------------------------

## 4. 예제

``` python
print(df.shape)
print(df.index)
print(df.columns)
```

실행 결과 예시:

``` text
(5, 2)
RangeIndex(start=0, stop=5, step=1)
Index(['one', 'two'], dtype='object')
```

### 코드 해석

- `(5, 2)` → 행 5개, 열 2개
- `RangeIndex(...)` → 0부터 4까지의 행 인덱스
- `Index(['one', 'two'], ...)` → 두 컬럼의 이름

> **결과 해석:** `stop=5`는 포함되지 않으므로 실제 행 인덱스는 0부터 4까지이다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | Series | DataFrame |
| --- | --- | --- |
| 차원 | 1차원 | 2차원 |
| 비유 | 벡터, 한 컬럼 | 행렬, 표 |
| 생성 | `pd.Series()` | `pd.DataFrame()` |
| 컬럼 축 | 없음 | 여러 컬럼을 가짐 |

------------------------------------------------------------------------

## 6. 주의할 점

- `shape`의 첫 번째 값은 행 개수, 두 번째 값은 열 개수이다.
- `RangeIndex`의 `stop` 값은 실제 인덱스에 포함되지 않는다.
- `index`와 `columns`는 메서드가 아닌 속성이므로 괄호 없이 접근한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `Series` | 1차원 Pandas 데이터 구조 |
| `DataFrame` | 행과 열로 구성된 2차원 Pandas 데이터 구조 |
| `Index` | 행을 구분하는 값 |
| `Column` | 변수 또는 특성을 나타내는 열 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `pd.Series(data=...)` | Series 생성 |
| `pd.DataFrame(data=...)` | DataFrame 생성 |
| `df.shape` | 행·열 개수 확인 |
| `df.index` | 행 인덱스 확인 |
| `df.columns` | 컬럼 이름 확인 |
| `df.info()` | 구조와 dtype 확인 |

### ⭐ 한 줄 정리

> **Series는 1차원 한 컬럼이고 DataFrame은 여러 Series가 모인 2차원 표이다.**

### 🔖 복습할 내용

- [ ] Series와 DataFrame의 차원 구분하기
- [ ] DataFrame Shape 읽기
- [ ] index·columns·info로 구조 확인하기
