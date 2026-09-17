---
source:
  - "[[02 정리노트/week04/day16_08.28]]"
---

# map과 apply

## 1. 개념

`Series.map()`은 Series의 각 값에 함수나 매핑 규칙을 적용한다. `DataFrame.apply(..., axis=1)`은 각 행을 Series로 전달하여 여러 컬럼을 함께 계산한다.

> **핵심:** 값 하나씩 바꿀 때는 map, 한 행의 여러 컬럼을 계산할 때는 DataFrame apply를 활용한다.

---

## 2. 쉽게 이해하기

map은 한 컬럼의 값을 하나씩 변환하고 apply(axis=1)는 표의 한 행 전체를 함수에 전달한다.

```text
Series 값 → map → 값별 변환
DataFrame 행 → apply(axis=1) → 여러 컬럼 계산
```

---

## 3. 사용 방법

```python
df["sex_code"] = df["sex"].map({"male": 0, "female": 1})
df["family_cnt"] = df.apply(family_count, axis=1)
```

- 매핑 딕셔너리는 기존 값을 새 값으로 바꾼다.
- `axis=1`이면 함수에 한 행을 나타내는 Series가 전달된다.
- Series에도 `apply()`를 사용할 수 있으므로 구분은 절대적인 규칙이 아니다.

---

## 4. 예제

```python
def family_count(row):
    return row["sibsp"] + row["parch"]

df["family_cnt"] = df.apply(family_count, axis=1)
```

각 행의 두 컬럼을 더해 가족 수 컬럼을 만든다.

---

## 5. 헷갈리는 개념 비교

|구분|`Series.map()`|`DataFrame.apply(axis=1)`|
|---|---|---|
|입력|값 하나|행 Series|
|활용|한 컬럼 값 변환|여러 컬럼을 함께 계산|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|값 변환|각 원소를 새 값으로 변경|
|행 연산|한 행의 여러 컬럼을 함께 계산|
|매핑 규칙|기존 값과 새 값의 대응 관계|

### 💻 주요 코드

|코드|의미|
|---|---|
|`series.map(mapping)`|값별 매핑 적용|
|`series.map(func)`|값별 함수 적용|
|`df.apply(func, axis=1)`|행별 함수 적용|

### ⭐ 한 줄 정리

> **map은 Series 값을 하나씩 변환하고 apply(axis=1)는 DataFrame의 각 행을 계산한다.**

### 🔖 복습할 내용

- [ ] map과 apply의 입력 단위 구분하기
- [ ] 매핑 딕셔너리로 범주 변환하기
- [ ] 여러 컬럼으로 새 컬럼 만들기
