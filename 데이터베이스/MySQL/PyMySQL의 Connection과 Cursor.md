# PyMySQL의 Connection과 Cursor

## 1. 개념

PyMySQL은 Python에서 MySQL 서버와 통신하는 드라이버이다. Connection은 서버와의 연결 세션을 관리하고, Cursor는 그 연결을 통해 SQL을 실행하고 결과를 읽는다.

> **핵심:** Connection이 통신 경로를 열고 Cursor가 그 경로를 이용해 SQL과 결과를 주고받는다.

------------------------------------------------------------------------

## 2. 연결 흐름

```text
접속 설정
  ↓
pymysql.connect()
  ↓
Connection
  ↓ cursor()
Cursor
  ↓ execute()
MySQL에서 SQL 실행
  ↓ fetchall()
Python으로 결과 반환
```

------------------------------------------------------------------------

## 3. 사용 방법

```python
import pymysql

db_config = {
    "host": "localhost",
    "port": 3306,
    "user": "root",
    "password": "비밀번호",
    "database": "classicmodels",
}

with pymysql.connect(**db_config) as conn:
    with conn.cursor() as cur:
        cur.execute("SHOW TABLES;")
        rows = cur.fetchall()
```

- `**db_config` → 딕셔너리의 키와 값을 키워드 인자로 전달한다.
- `execute()` → SQL을 서버에서 실행한다.
- `fetchall()` → 조회 결과의 남은 행을 모두 가져온다.
- `with` → 블록 종료 시 자원을 정리한다.

------------------------------------------------------------------------

## 4. DictCursor

```python
conn = pymysql.connect(
    **db_config,
    charset="utf8mb4",
    cursorclass=pymysql.cursors.DictCursor,
)
```

`DictCursor`를 사용하면 한 행이 컬럼 순서 기반의 튜플이 아니라 컬럼 이름을 키로 가진 딕셔너리로 표현된다. 따라서 `row["customerName"]`처럼 의미가 드러나는 방식으로 값을 읽을 수 있다.

------------------------------------------------------------------------

## 5. 주의할 점

- 비밀번호를 소스 코드에 직접 작성하지 말고 환경 변수로 분리한다.
- Connection과 Cursor는 사용이 끝나면 닫아야 하므로 `with`문으로 정리한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| PyMySQL | Python과 MySQL을 연결하는 드라이버이다. |
| Connection | 서버 연결과 트랜잭션을 관리한다. |
| Cursor | SQL을 실행하고 결과를 가져온다. |

### ⭐ 한 줄 정리

> **PyMySQL에서는 Connection으로 서버에 연결하고 Cursor로 SQL을 실행해 결과를 가져온다.**

### 🔖 복습할 내용

- [ ] Connection과 Cursor의 역할 구분하기
- [ ] `execute()`와 `fetchall()`의 실행 순서 설명하기
- [ ] DictCursor 결과 형태 확인하기
