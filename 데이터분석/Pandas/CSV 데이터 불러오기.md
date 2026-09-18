---
source:
  - "[[02 정리노트/week03/day11_08.21]]"
---

# CSV 데이터 불러오기

## 1. 개념

CSV 파일은 Pandas의 `read_csv()`로 DataFrame에 불러온다. 파일 인코딩과 컬럼 자료형을 올바르게 지정하고 불러온 직후 구조를 확인해야 한다.

> **핵심:** CSV를 읽은 뒤 행 개수와 dtype을 확인하고 식별 코드처럼 계산하지 않는 값은 문자열로 보존한다.

---

## 2. 쉽게 이해하기

파일을 열기만 하는 것이 아니라 문자 해석 방식과 각 컬럼의 값 종류를 함께 지정하는 과정이다.

```text
glob으로 파일 찾기 → read_csv() → info()로 구조 확인
```

---

## 3. 사용 방법

```python
import glob
import pandas as pd

csv_files = glob.glob("*.csv")
df = pd.read_csv("data.csv", encoding="utf-8", dtype={"지역코드": "string"})
df.info()
```

- `*` → 파일명의 여러 문자를 대신하는 와일드카드이다.
- `encoding` → 파일 문자 인코딩을 지정한다.
- `dtype` → 컬럼을 읽을 자료형을 지정한다.
- `info()` → 행, 컬럼, 결측이 아닌 값과 자료형을 확인한다.

---

## 4. 예제

```python
import pandas as pd

df = pd.read_csv(
    "data.csv",
    encoding="utf-8",
    dtype={"지역코드": "string"},
)
```

지역 코드 `01`은 계산값이 아니라 식별값이므로 문자열로 읽어 앞의 `0`을 보존한다. `RangeIndex: 100 entries, 0 to 99`는 행이 100개임을 뜻한다.

---

## 5. 헷갈리는 개념 비교

|구분|계산값|코드값|
|---|---|---|
|용도|크기와 연산|대상 식별|
|자료형 예시|정수·실수|문자열|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|인코딩|문자를 바이트로 표현하는 방식|
|`dtype`|컬럼 값의 자료형|
|`RangeIndex`|DataFrame의 기본 행 인덱스 범위|

### 💻 주요 코드

|코드|의미|
|---|---|
|`glob.glob("*.csv")`|CSV 파일 경로 검색|
|`pd.read_csv()`|CSV를 DataFrame으로 읽기|
|`df.info()`|DataFrame 구조 확인|

### ⭐ 한 줄 정리

> **CSV는 인코딩과 dtype을 맞춰 읽고 DataFrame 구조를 즉시 검증한다.**

### 🔖 복습할 내용

- [ ] 와일드카드로 CSV 찾기
- [ ] 코드값을 문자열로 읽는 이유 설명하기
- [ ] `df.info()` 결과 해석하기
