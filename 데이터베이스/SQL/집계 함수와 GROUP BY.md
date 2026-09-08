# 집계 함수와 GROUP BY

## 1. 개념

집계 함수는 여러 행을 개수, 합계 같은 하나의 요약 값으로 계산한다. `GROUP BY`는 같은 기준값을 가진 행을 그룹으로 묶어 그룹마다 집계 결과를 구할 때 사용한다.

> **핵심:** 전체를 한 번 집계할지 기준별로 나누어 집계할지는 `GROUP BY`의 유무가 결정한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

주문서를 고객 번호별로 묶은 뒤 각 묶음의 장수를 세면 고객별 주문 횟수가 된다.

```text
여러 주문 행
  ↓ customerNumber로 그룹화
고객별 주문 그룹
  ↓ COUNT 또는 SUM
고객별 요약 값
```

------------------------------------------------------------------------

## 3. 사용 방법

```sql
SELECT
    customerNumber,
    COUNT(orderNumber) AS order_count
FROM orders
GROUP BY customerNumber
ORDER BY order_count DESC;
```

- `COUNT(orderNumber)` → `NULL`이 아닌 주문 번호의 개수를 센다.
- `SUM(expression)` → 그룹에 속한 계산값을 모두 더한다.
- `GROUP BY customerNumber` → 고객 번호별로 행을 묶는다.

------------------------------------------------------------------------

## 4. 예제

```sql
SELECT
    o.customerNumber,
    SUM(od.quantityOrdered * od.priceEach) AS customer_total
FROM orders AS o
JOIN orderdetails AS od
    ON o.orderNumber = od.orderNumber
GROUP BY o.customerNumber
ORDER BY customer_total DESC;
```

### 코드 해석

- 수량과 가격을 곱해 주문 상품 한 행의 금액을 계산한다.
- 고객 번호별로 행을 묶고 `SUM()`으로 구매 금액을 더한다.
- 계산된 총액이 큰 고객부터 정렬한다.

------------------------------------------------------------------------

## 5. 주의할 점

- `COUNT(column)`은 해당 컬럼이 `NULL`인 행을 세지 않지만 `COUNT(*)`는 행 자체를 센다.
- `GROUP BY`가 있는 조회문에서 집계하지 않는 컬럼은 그룹 기준과 일치하도록 작성한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| 집계 함수 | 여러 행을 하나의 요약 값으로 계산한다. |
| `GROUP BY` | 같은 기준값의 행을 그룹으로 묶는다. |
| 별칭 | 계산 결과에 읽기 쉬운 이름을 붙인다. |

### ⭐ 한 줄 정리

> **GROUP BY로 기준별 그룹을 만들고 COUNT나 SUM으로 각 그룹을 요약한다.**

### 🔖 복습할 내용

- [ ] `COUNT(*)`와 `COUNT(column)`의 차이 확인하기
- [ ] 고객별 합계 쿼리 작성하기
- [ ] 집계할 컬럼과 그룹 기준 구분하기
