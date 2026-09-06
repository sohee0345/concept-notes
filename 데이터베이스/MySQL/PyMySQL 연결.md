# PyMySQL 연결

## 1. 개념

PyMySQL은 Python 프로그램에서 MySQL 서버에 연결하고 SQL을 실행할 때 사용하는 드라이버이다. Connection으로 서버에 연결하고 Cursor로 SQL을 전달해 결과를 가져온다.

> **핵심:** 접속 설정으로 Connection을 만들고 Cursor의 `execute()`와 `fetchall()`로 SQL 결과를 받는다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
Python
  ↓ Connection으로 MySQL 연결
Cursor로 SQL 전달
  ↓
MySQL에서 SQL 실행
  ↓ fetchall()
Python으로 결과 반환
```

> **쉽게 말하면:** Connection은 서버와 이어진 통로이고 Cursor는 그 통로로 SQL과 결과를 주고받는 도구이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
import pymysql

DB_CONFIG = {
    "host": "localhost",
    "port": 3306,
    "user": "root",
    "password": "root1234",
    "database": "classicmodels",
}

with pymysql.connect(**DB_CONFIG) as conn:
    with conn.cursor() as cur:
        cur.execute("SHOW TABLES;")
        results = cur.fetchall()
```

- `pymysql.connect()` → Connection 생성
- `**DB_CONFIG` → 설정 딕셔너리를 키워드 인자로 전달
- `cursor()` → Cursor 생성
- `execute()` → SQL 실행
- `fetchall()` → 모든 결과 조회

> **핵심:** `with` 블록을 사용해 Connection과 Cursor 자원을 사용 후 정리한다.

------------------------------------------------------------------------

## 4. 예제

``` python
class MySQLDB:
    def __init__(self, db_config: dict) -> None:
        self.conn = pymysql.connect(
            **db_config,
            charset="utf8mb4",
            cursorclass=pymysql.cursors.DictCursor,
        )

    def __call__(self, query: str):
        with self.conn.cursor() as cur:
            cur.execute(query=query)
            return cur.fetchall()

mysqldb = MySQLDB(DB_CONFIG)
results = mysqldb("SELECT * FROM customers;")
```

### 코드 해석

- `charset="utf8mb4"` → 한글 등을 처리할 문자 집합 지정
- `DictCursor` → 컬럼 이름을 키로 가진 딕셔너리 형태의 행 반환
- `__call__()` → 객체를 함수처럼 호출해 SQL 실행

> **결과 해석:** `mysqldb("SQL")` 형태로 쿼리를 전달하고 딕셔너리 기반 결과를 받아 DataFrame 등으로 변환할 수 있다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | Connection | Cursor |
| --- | --- | --- |
| 역할 | Python과 MySQL 연결 | SQL 전달과 결과 수신 |
| 생성 | `pymysql.connect()` | `conn.cursor()` |
| 주요 작업 | 접속 설정 유지 | `execute()`, `fetchall()` |

------------------------------------------------------------------------

## 6. 주의할 점

- host, port, user, password, database 설정을 모두 확인한다.
- 설정 딕셔너리의 각 항목은 쉼표로 구분한다.
- Connection과 Cursor는 사용 후 정리한다.
- 접속 비밀번호를 코드와 저장소에 그대로 남기지 않는다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `PyMySQL` | Python과 MySQL을 연결하는 드라이버 |
| `Connection` | MySQL 서버 연결 객체 |
| `Cursor` | SQL 실행과 결과 조회 객체 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `pymysql.connect()` | Connection 생성 |
| `conn.cursor()` | Cursor 생성 |
| `cur.execute()` | SQL 실행 |
| `cur.fetchall()` | 결과 전체 조회 |
| `pymysql.cursors.DictCursor` | 딕셔너리 형태 결과 설정 |

### ⭐ 한 줄 정리

> **PyMySQL은 Connection으로 MySQL에 연결하고 Cursor로 SQL을 실행해 결과를 가져온다.**

### 🔖 복습할 내용

- [ ] DB_CONFIG 필수 항목 작성하기
- [ ] Connection과 Cursor 역할 비교하기
- [ ] 조회 결과를 DataFrame으로 변환하기
