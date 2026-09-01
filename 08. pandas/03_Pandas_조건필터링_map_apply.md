# Pandas 조건 필터링 · map · apply

## 1. 개념

Pandas에서는 Boolean 조건을 만들어 원하는 행만 선택할 수 있다.

`map()`은 주로 Series의 각 값에 함수를 적용할 때 사용하고, `apply()`는 여러 컬럼이나 행·열 단위 처리가 필요할 때 사용할 수 있다.

> **핵심:** Pandas에서는 Boolean 조건으로 데이터를 필터링하고 map/apply로 데이터에 함수를 적용할 수 있다.

---

## 2. 쉽게 이해하기

조건식은 각 행마다 `True` 또는 `False`를 만든다.

```text
조건 만족 → True  → 선택
조건 불만족 → False → 제외
```

`~`를 붙이면 True/False가 반대로 뒤집힌다.

---

## 3. 사용 방법

```python
cond = (
    iris["sepal_width"].isin([3.5, 3.2])
) & (
    iris["species"] == "setosa"
)

iris[cond]
iris[~cond]
```

```python
iris["sepal_width"].map(lambda x: x * 2)
```

---

## 4. 예제

```python
df["age"].map(lambda x: (x // 10) * 10)
```

→ 각 나이를 10대, 20대, 30대처럼 묶는 값을 만들 수 있다.

---

## 5. 헷갈리는 개념 비교

| 구분 | `map()` | `apply()` |
|---|---|---|
| 기본 사용 | Series 각 값 | 행·열 또는 여러 컬럼 처리 |
| 초반 기억법 | 컬럼 하나 | 여러 컬럼/행·열 |

※ `apply()`도 Series에 사용할 수 있으므로 절대적인 구분은 아니다.

---

## 🟦 핵심 정리

### 💡 주요 개념

- `isin()` → 여러 값 중 포함 여부
- `&` → AND
- `|` → OR
- `~` → NOT
- `map()` → 각 값에 함수 적용

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `df[cond]` | 조건 만족 행 선택 |
| `df[~cond]` | 조건 불만족 행 선택 |
| `Series.isin()` | 값 포함 여부 확인 |
| `Series.map()` | 각 값에 함수 적용 |
| `DataFrame.apply()` | 행·열 단위 함수 적용 |

### ⭐ 한 줄 정리

> **Pandas에서는 Boolean 조건으로 데이터를 필터링하고 map/apply로 데이터에 함수를 적용할 수 있다.**

### 🔖 복습할 내용

- [ ] `&`, `|`, `~` 의미
- [ ] `isin()` 사용법
- [ ] `map()`과 `apply()` 사용 기준
