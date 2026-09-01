# Python · MySQL 연동과 .env

## 1. 개념

Python에서는 `pymysql`을 사용해 MySQL에 연결할 수 있다.

DB 비밀번호나 API Key처럼 중요한 값은 코드에 직접 작성하지 않고 `.env` 파일에 분리하여 관리한다.

> **핵심:** Python은 pymysql로 MySQL에 연결하고, 민감한 접속정보는 .env로 분리해 관리한다.

---

## 2. 쉽게 이해하기

연결 과정을 전화에 비유하면:

```text
Connection → MySQL과 연결
Cursor     → 연결된 MySQL에 SQL 전달
execute()  → SQL 실행
fetchall() → 결과 가져오기
```

`.env`는 비밀번호를 소스코드 밖에 따로 보관하는 파일이라고 생각하면 된다.

---

## 3. 사용 방법

```python
import pymysql
import os
from dotenv import load_dotenv

load_dotenv()

DB_CONFIG = {
    "host": os.getenv("host"),
    "port": int(os.getenv("port")),
    "user": os.getenv("user"),
    "password": os.getenv("password"),
    "database": os.getenv("database")
}

with pymysql.connect(**DB_CONFIG) as conn:
    with conn.cursor() as cur:
        cur.execute("SHOW TABLES;")
        results = cur.fetchall()
```

---

## 4. 예제

```text
.env
 ↓
load_dotenv()
 ↓
환경변수 등록
 ↓
os.getenv()
 ↓
DB_CONFIG
 ↓
pymysql.connect()
```

---

## 5. 헷갈리는 개념 비교

| 구분 | 의미 |
|---|---|
| Connection | Python ↔ MySQL 연결 |
| Cursor | SQL 전달·결과 수신 |
| `.env` | 민감정보 저장 |
| `load_dotenv()` | `.env` 값을 환경변수로 등록 |
| `os.getenv()` | 환경변수 값 가져오기 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- `pymysql` → Python-MySQL 연결
- `with` → 사용 후 자원 자동 정리
- `.env` → 비밀번호 등 민감정보 분리

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `pymysql.connect(**DB_CONFIG)` | MySQL 연결 |
| `conn.cursor()` | Cursor 생성 |
| `cur.execute()` | SQL 실행 |
| `cur.fetchall()` | 결과 전체 조회 |
| `load_dotenv()` | `.env` 로드 |
| `os.getenv()` | 환경변수 조회 |

### ⭐ 한 줄 정리

> **Python은 pymysql로 MySQL에 연결하고, 민감한 접속정보는 .env로 분리해 관리한다.**

### 🔖 복습할 내용

- [ ] Connection과 Cursor 차이
- [ ] `.env → load_dotenv → os.getenv` 흐름
- [ ] `with`문을 사용하는 이유
