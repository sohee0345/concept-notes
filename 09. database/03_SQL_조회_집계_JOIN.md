# SQL 조회 · 집계 · JOIN

## 1. 개념

SQL 조회에서는 `WHERE`, `ORDER BY`, `LIMIT`으로 원하는 데이터를 걸러내고, `COUNT`, `SUM`, `GROUP BY`로 데이터를 집계할 수 있다.

`JOIN`은 서로 다른 테이블을 공통 컬럼을 기준으로 연결할 때 사용한다.

> **핵심:** 복잡한 SQL은 작은 조회·집계 쿼리를 만든 뒤 JOIN과 서브쿼리로 연결하면 이해하기 쉽다.

---

## 2. 쉽게 이해하기

예를 들어 고객 테이블과 주문 테이블이 따로 있다면, 고객 번호를 기준으로 연결해서 '누가 몇 번 주문했는지'를 확인할 수 있다.

```text
customers
    ↘ customerNumber
      JOIN
    ↗ customerNumber
orders
```

---

## 3. 사용 방법

```sql
SELECT
    customerNumber,
    COUNT(orderNumber) AS cnt
FROM orders
GROUP BY customerNumber
ORDER BY cnt DESC
LIMIT 3;
```

```sql
SELECT t1.customerName, t2.cnt
FROM customers t1
JOIN (
    SELECT customerNumber, COUNT(orderNumber) AS cnt
    FROM orders
    GROUP BY customerNumber
) t2
ON t1.customerNumber = t2.customerNumber;
```

---

## 4. 예제

고객별 총 주문 금액은 먼저 주문 상세에서 금액을 계산한 뒤, 주문 테이블과 연결해서 고객별로 합계를 낸다.

```sql
quantityOrdered * priceEach
```

```text
상품 금액 계산
→ 주문과 JOIN
→ 고객별 GROUP BY
→ SUM()
```

---

## 5. 헷갈리는 개념 비교

| 구분 | 역할 |
|---|---|
| `WHERE` | 조건 필터링 |
| `GROUP BY` | 같은 값끼리 묶기 |
| `ORDER BY` | 결과 정렬 |
| `JOIN` | 테이블 연결 |
| 서브쿼리 | SQL 안에 들어가는 SQL |

---

## 🟦 핵심 정리

### 💡 주요 개념

- `COUNT()` → 개수
- `SUM()` → 합계
- `GROUP BY` → 그룹화
- Alias → 테이블/컬럼 별명
- JOIN → 공통 컬럼 기준 연결

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `WHERE country='USA'` | 조건에 맞는 행 조회 |
| `ORDER BY ... DESC` | 내림차순 정렬 |
| `LIMIT 3` | 상위 3개만 조회 |
| `COUNT()` | 개수 집계 |
| `SUM()` | 합계 집계 |
| `JOIN ... ON ...` | 테이블 연결 |

### ⭐ 한 줄 정리

> **복잡한 SQL은 작은 조회·집계 쿼리를 만든 뒤 JOIN과 서브쿼리로 연결하면 이해하기 쉽다.**

### 🔖 복습할 내용

- [ ] `WHERE`/`GROUP BY` 차이
- [ ] JOIN의 `ON` 조건
- [ ] 서브쿼리와 Alias 구조
