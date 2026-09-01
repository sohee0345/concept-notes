# Pandas Series · DataFrame · Index

## 1. 개념

Pandas의 대표적인 데이터 구조는 `Series`와 `DataFrame`이다.

Series는 1차원, DataFrame은 2차원 데이터이며 DataFrame의 각 행은 `Index`로 구분한다.

> **핵심:** Series는 1차원, DataFrame은 2차원이며 Index는 각 행을 구분한다.

---

## 2. 쉽게 이해하기

```text
Series    → 한 줄 데이터 → 1차원
DataFrame → 행과 열      → 2차원
```

DataFrame에서 Row는 관측값 한 건, Column은 각 데이터가 가진 변수라고 생각하면 된다.

---

## 3. 사용 방법

```python
iris.index
```

결과 예:

```text
RangeIndex(start=0, stop=150, step=1)
```

실제 인덱스는 `0 ~ 149`이며 총 150개의 행이다.

---

## 4. 예제

Shape이 `(150, 5)`라면:

```text
150 → row 개수
5   → column 개수
```

---

## 5. 헷갈리는 개념 비교

| 구분 | Series | DataFrame |
|---|---|---|
| 차원 | 1차원 | 2차원 |
| 비유 | 벡터 | 행렬 |
| 구성 | 값 + Index | Row + Column + Index |

---

## 🟦 핵심 정리

### 💡 주요 개념

- Series → 1차원
- DataFrame → 2차원
- Row → 관측값
- Column → 변수
- Index → 행 구분 값

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `iris.index` | Index 확인 |
| `df.shape` | 행·열 크기 확인 |

### ⭐ 한 줄 정리

> **Series는 1차원, DataFrame은 2차원이며 Index는 각 행을 구분한다.**

### 🔖 복습할 내용

- [ ] Series와 DataFrame 차이
- [ ] `(150, 5)` Shape 해석
- [ ] `stop` 값이 포함되지 않는다는 점
