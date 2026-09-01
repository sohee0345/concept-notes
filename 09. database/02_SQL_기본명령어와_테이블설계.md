# SQL 기본 명령어와 테이블 설계

## 1. 개념

SQL에서는 데이터베이스를 선택하고 테이블을 생성·삭제하며 데이터를 추가·조회할 수 있다.

테이블을 만들 때는 컬럼의 데이터 타입과 `NOT NULL`, `DEFAULT`, `PRIMARY KEY`, `AUTO_INCREMENT` 같은 옵션을 함께 지정한다.

> **핵심:** SQL의 기본 흐름은 DB 선택 → 테이블 생성 → 데이터 추가 → 데이터 조회이다.

---

## 2. 쉽게 이해하기

테이블을 엑셀 표라고 생각하면 쉽다.

```text
CREATE TABLE → 빈 표 만들기
INSERT INTO  → 행 추가하기
SELECT       → 내용 보기
DROP TABLE   → 표 삭제하기
```

---

## 3. 사용 방법

```sql
USE examplesdb;

CREATE TABLE userdb (
    id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(20) DEFAULT '없음',
    addr VARCHAR(500) NOT NULL,
    PRIMARY KEY(id)
);

INSERT INTO userdb (name, addr)
VALUES ('홍길동', '서울시 강남구');

SELECT * FROM userdb;
```

---

## 4. 예제

`AUTO_INCREMENT`가 있으면 `id` 값을 직접 넣지 않아도 자동으로 증가한다.

```text
첫 번째 INSERT → id 1
두 번째 INSERT → id 2
세 번째 INSERT → id 3
```

---

## 5. 헷갈리는 개념 비교

| 개념 | 의미 |
|---|---|
| `NOT NULL` | 반드시 값이 필요 |
| `DEFAULT` | 값이 없을 때 기본값 사용 |
| `PRIMARY KEY` | 각 행을 고유하게 식별 |
| `AUTO_INCREMENT` | 숫자 자동 증가 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- `PRIMARY KEY` → 중복 X, NULL X
- `VARCHAR(n)` → 문자열 타입
- `AUTO_INCREMENT` → id 자동 증가
- `IF EXISTS` → 존재할 때만 실행

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `USE db;` | 사용할 DB 선택 |
| `CREATE TABLE` | 테이블 생성 |
| `DROP TABLE IF EXISTS` | 테이블이 있을 때 삭제 |
| `INSERT INTO` | 데이터 추가 |
| `SELECT` | 데이터 조회 |

### ⭐ 한 줄 정리

> **SQL의 기본 흐름은 DB 선택 → 테이블 생성 → 데이터 추가 → 데이터 조회이다.**

### 🔖 복습할 내용

- [ ] `PRIMARY KEY` 조건
- [ ] `NOT NULL`과 `DEFAULT` 차이
- [ ] `AUTO_INCREMENT` 사용법
