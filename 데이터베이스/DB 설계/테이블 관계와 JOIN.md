# 테이블 관계와 JOIN

## 1. 개념

관계형 데이터베이스는 기본키와 외래키로 여러 테이블을 연결한다. 1:N 관계는 부모 한 행에 자식 여러 행이 연결되고, N:M 관계는 연결 테이블을 두어 두 개의 1:N 관계로 나눈다. JOIN은 연결된 데이터를 함께 조회한다.

> **핵심:** 외래키로 관계를 저장하고 JOIN으로 여러 테이블에 흩어진 정보를 합쳐 조회한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
students 1 ── N enrollments N ── 1 courses
                       │
                       1
                       │
                       N
                    payments
```

> **쉽게 말하면:** 각 표에는 자기 데이터만 저장하고, ID로 서로 연결한 뒤 조회할 때 필요한 정보를 합친다.

------------------------------------------------------------------------

## 3. 사용 방법

``` sql
CREATE TABLE enrollments (
    enrollment_id INT AUTO_INCREMENT,
    student_id INT NOT NULL,
    course_id INT NOT NULL,
    PRIMARY KEY (enrollment_id),
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

- `students → enrollments` → 1:N
- `courses → enrollments` → 1:N
- `students ↔ courses` → 연결 테이블을 통한 N:M

> **핵심:** 연결 테이블에는 양쪽 부모 테이블을 참조하는 외래키를 둔다.

------------------------------------------------------------------------

## 4. 예제

``` sql
SELECT
    s.name AS student_name,
    c.title AS course_title,
    e.status,
    p.amount
FROM enrollments e
JOIN students s ON e.student_id = s.student_id
JOIN courses c ON e.course_id = c.course_id
LEFT JOIN payments p ON e.enrollment_id = p.enrollment_id
ORDER BY s.name, c.title;
```

### 코드 해석

- `enrollments e` → `enrollments`에 별칭 `e` 지정
- `JOIN ... ON` → 키가 일치하는 행 연결
- `LEFT JOIN payments` → 결제가 없어도 수강 신청 행은 유지
- `ORDER BY` → 학생과 강의 이름 기준 정렬

> **결과 해석:** 수강 신청을 중심으로 학생, 강의, 결제 정보를 한 결과에서 확인한다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | 1:N | N:M |
| --- | --- | --- |
| 의미 | 부모 한 행과 자식 여러 행 | 양쪽 모두 여러 행과 연결 |
| 예시 | 수강 신청 1건과 여러 결제 | 여러 학생과 여러 강의 |
| 구현 | 자식 테이블에 외래키 | 연결 테이블에 양쪽 외래키 |

------------------------------------------------------------------------

## 6. 주의할 점

- 부모 데이터를 먼저 추가한 뒤 이를 참조하는 자식 데이터를 추가한다.
- 삭제는 의존 관계의 반대 순서로 자식 테이블부터 진행한다.
- `ON DELETE CASCADE`는 관련 자식 행도 삭제하므로 영향을 확인한다.
- `ON DELETE RESTRICT`는 참조 중인 자식 행이 있으면 부모 삭제를 막는다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `1:N` | 부모 한 행에 자식 여러 행이 연결되는 관계 |
| `N:M` | 양쪽 모두 여러 행과 연결되는 관계 |
| `연결 테이블` | N:M 관계를 두 개의 1:N으로 나누는 테이블 |
| `JOIN` | 관계가 있는 테이블의 행을 함께 조회하는 연산 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `FOREIGN KEY` | 다른 테이블의 키 참조 |
| `JOIN ... ON` | 일치하는 관련 행 연결 |
| `LEFT JOIN` | 왼쪽 행을 유지하며 오른쪽 데이터 연결 |
| `ON DELETE CASCADE` | 부모 삭제 시 관련 자식도 삭제 |
| `ON DELETE RESTRICT` | 참조 중인 부모 삭제 제한 |

### ⭐ 한 줄 정리

> **기본키와 외래키로 테이블 관계를 만들고 JOIN으로 연결된 데이터를 함께 조회한다.**

### 🔖 복습할 내용

- [ ] 1:N 관계 예시 그리기
- [ ] N:M 관계를 연결 테이블로 바꾸기
- [ ] JOIN과 LEFT JOIN의 차이 확인하기
