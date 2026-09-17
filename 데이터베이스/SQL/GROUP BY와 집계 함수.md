---
source:
  - "[[02 정리노트/week03/day10_08.20]]"
---

# GROUP BY와 집계 함수

## 1. 개념

집계 함수는 여러 행을 개수나 합계 같은 하나의 값으로 요약한다. `GROUP BY`는 같은 기준값을 가진 행을 묶어 그룹별 집계 결과를 만든다.

> **핵심:** GROUP BY로 행을 기준별로 묶고 집계 함수로 각 그룹을 요약한다.

---

## 2. 쉽게 이해하기

고객별로 주문 영수증을 모은 뒤 각 묶음의 개수나 금액 합계를 계산하는 과정이다.

```text
행 모음
  ↓ GROUP BY
기준별 그룹
  ↓ COUNT·SUM
그룹별 요약 값
```

---

## 3. 사용 방법

```sql
SELECT customerNumber, COUNT(orderNumber) AS order_count
FROM orders
GROUP BY customerNumber;
```

- `COUNT()` → 행이나 값의 개수를 센다.
- `SUM()` → 값의 합계를 구한다.
- `GROUP BY` → 같은 기준값의 행을 묶는다.
- `AS` → 계산 결과에 별칭을 붙인다.

---

## 4. 예제

```sql
SELECT
    o.customerNumber,
    SUM(od.quantityOrdered * od.priceEach) AS customer_total
FROM orders AS o
JOIN orderdetails AS od ON o.orderNumber = od.orderNumber
GROUP BY o.customerNumber
ORDER BY customer_total DESC;
```

주문 상세 금액을 계산한 뒤 고객별로 합산하고 큰 금액부터 정렬한다.

---

## 5. 헷갈리는 개념 비교

|구분|WHERE|GROUP BY|
|---|---|---|
|역할|그룹화 전 행 필터링|같은 기준값으로 행 묶기|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|집계 함수|여러 행을 하나의 값으로 요약|
|그룹화|같은 기준의 행을 묶는 작업|
|별칭|결과 컬럼이나 테이블에 붙인 이름|

### 💻 주요 코드

|코드|의미|
|---|---|
|`COUNT()`|개수 계산|
|`SUM()`|합계 계산|
|`GROUP BY 컬럼`|컬럼값별 그룹 생성|

### ⭐ 한 줄 정리

> **GROUP BY와 집계 함수는 데이터를 기준별로 묶어 개수와 합계 같은 요약 결과를 만든다.**

### 🔖 복습할 내용

- [ ] COUNT와 SUM 구분하기
- [ ] 고객별 집계 쿼리 작성하기
- [ ] 집계하지 않는 컬럼과 그룹 기준 맞추기
