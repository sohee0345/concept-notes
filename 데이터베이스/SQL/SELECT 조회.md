---
source:
  - "[[02 정리노트/week03/day10_08.20]]"
---

# SELECT 조회

## 1. 개념

`SELECT`는 테이블에서 필요한 컬럼과 행을 조회하는 SQL문이다. `WHERE`, `ORDER BY`, `LIMIT`을 조합해 조건·정렬·결과 개수를 지정한다.

> **핵심:** 조회 대상과 행 조건, 정렬 기준, 반환 개수를 단계적으로 지정한다.

---

## 2. 쉽게 이해하기

전체 자료에서 표를 고르고, 필요한 행만 거른 뒤, 보여 줄 컬럼과 순서를 정하는 과정이다.

```text
FROM → WHERE → SELECT → ORDER BY → LIMIT
```

---

## 3. 사용 방법

```sql
SELECT customerName, country, creditLimit
FROM customers
WHERE country = 'USA'
ORDER BY creditLimit DESC
LIMIT 10;
```

- `SELECT` → 표시할 컬럼이나 계산식을 정한다.
- `FROM` → 조회할 테이블을 정한다.
- `WHERE` → 행 단위 조건을 적용한다.
- `ORDER BY` → 정렬 기준을 정한다.
- `LIMIT` → 반환할 행 수를 제한한다.

---

## 4. 예제

```sql
SELECT customerName, phone
FROM customers
WHERE country = 'USA'
ORDER BY customerName ASC
LIMIT 3;
```

미국 고객만 이름순으로 정렬하여 처음 세 행을 조회한다.

---

## 5. 헷갈리는 개념 비교

|구분|작성 순서|논리적 처리 순서|
|---|---|---|
|순서|SELECT → FROM → WHERE|FROM → WHERE → SELECT|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|조회|테이블에서 필요한 데이터를 선택하는 작업|
|필터링|조건에 맞는 행만 남기는 작업|
|정렬|지정한 기준으로 결과 순서를 정하는 작업|

### 💻 주요 코드

|코드|의미|
|---|---|
|`WHERE 조건`|행 필터링|
|`ORDER BY 컬럼 DESC`|내림차순 정렬|
|`LIMIT n`|결과 행 수 제한|

### ⭐ 한 줄 정리

> **SELECT 조회는 테이블에서 조건에 맞는 데이터를 선택하고 정렬과 개수 제한을 적용한다.**

### 🔖 복습할 내용

- [ ] 각 절의 역할 설명하기
- [ ] 작성 순서와 처리 순서 구분하기
- [ ] 상위 N개 행 조회하기
