---
source:
  - "[[02 정리노트/week03/day09_08.19]]"
---

# JOIN

## 1. 개념

JOIN은 관계로 나뉜 여러 테이블의 행을 연결하여 하나의 조회 결과로 만드는 SQL 기능이다.

> **핵심:** JOIN은 외래키와 기본키의 대응 조건을 이용해 관련 데이터를 한 결과로 결합한다.

---

## 2. 쉽게 이해하기

서로 다른 명부에 있는 고유 번호를 기준으로 같은 대상의 정보를 한 줄에 모으는 과정이다.

```text
왼쪽 테이블
  + 연결 조건
오른쪽 테이블
  ↓
결합된 조회 결과
```

---

## 3. 사용 방법

```sql
SELECT s.name, e.status
FROM enrollments e
JOIN students s ON e.student_id = s.student_id;
```

- `JOIN` → 양쪽에 대응하는 행이 있는 데이터만 연결한다.
- `LEFT JOIN` → 왼쪽 행을 모두 유지하고 오른쪽 대응 값이 있으면 연결한다.
- `ON` → 두 테이블을 연결할 조건을 지정한다.

---

## 4. 예제

```sql
SELECT
    s.name,
    c.title,
    p.amount
FROM enrollments e
JOIN students s ON e.student_id = s.student_id
JOIN courses c ON e.course_id = c.course_id
LEFT JOIN payments p ON e.enrollment_id = p.enrollment_id;
```

학생과 강의는 반드시 대응하는 행만 연결하고 결제가 없는 신청도 유지하도록 결제에는 LEFT JOIN을 사용한다.

---

## 5. 헷갈리는 개념 비교

|구분|JOIN|LEFT JOIN|
|---|---|---|
|결과|양쪽에 대응하는 행만|왼쪽 행은 모두 유지|
|오른쪽 대응 없음|제외|NULL로 표시|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|JOIN|관련 테이블의 행 결합|
|연결 조건|테이블 사이에서 대응할 키 조건|
|LEFT JOIN|왼쪽 행을 모두 유지하는 조인|

### 💻 주요 코드

|코드|의미|
|---|---|
|`JOIN table ON 조건`|대응 행만 연결|
|`LEFT JOIN table ON 조건`|왼쪽 행을 모두 유지하며 연결|

### ⭐ 한 줄 정리

> **JOIN은 테이블의 키 관계를 기준으로 나뉜 데이터를 하나의 조회 결과로 연결한다.**

### 🔖 복습할 내용

- [ ] JOIN과 LEFT JOIN 비교하기
- [ ] 기본키와 외래키로 연결 조건 작성하기
- [ ] 여러 테이블을 순서대로 조인하기
