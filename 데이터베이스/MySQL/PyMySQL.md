---
source:
  - "[[02 정리노트/week03/day10_08.20]]"
---

# PyMySQL

## 1. 개념

PyMySQL은 Python 프로그램이 MySQL 서버와 통신하게 하는 드라이버이다. Connection은 연결 세션을 관리하고 Cursor는 SQL을 실행하고 결과를 가져온다.

> **핵심:** Connection은 서버 연결을, Cursor는 SQL 실행과 결과 조회를 담당한다.

---

## 2. 쉽게 이해하기

Connection이 Python과 MySQL 사이의 통로라면 Cursor는 그 통로로 SQL을 전달하고 결과를 받아오는 작업자이다.

```text
Python → Connection → Cursor → MySQL
                         ↓
                    조회 결과 반환
```

---

## 3. 사용 방법

```python
import pymysql

with pymysql.connect(**DB_CONFIG) as conn:
    with conn.cursor() as cur:
        cur.execute("SHOW TABLES;")
        results = cur.fetchall()
```

- `pymysql.connect()` → Connection을 생성한다.
- `cursor()` → SQL 실행용 Cursor를 만든다.
- `execute()` → SQL을 서버에 전달해 실행한다.
- `fetchall()` → 남은 결과 행을 모두 가져온다.

---

## 4. 예제

```python
conn = pymysql.connect(
    **DB_CONFIG,
    charset="utf8mb4",
    cursorclass=pymysql.cursors.DictCursor,
)
```

`DictCursor`를 지정하면 각 행을 컬럼 이름이 키인 딕셔너리로 받을 수 있다. `with`문을 사용하면 블록 종료 시 연결 자원을 정리하기 쉽다.

---

## 5. 헷갈리는 개념 비교

|구분|Connection|Cursor|
|---|---|---|
|역할|MySQL 연결 세션 관리|SQL 실행과 결과 조회|
|생성|`pymysql.connect()`|`conn.cursor()`|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|드라이버|Python과 데이터베이스의 통신을 지원하는 라이브러리|
|Connection|서버 연결 세션|
|Cursor|SQL 실행과 결과 조회 객체|

### 💻 주요 코드

|코드|의미|
|---|---|
|`pymysql.connect(**DB_CONFIG)`|MySQL 연결 생성|
|`cur.execute(query)`|SQL 실행|
|`cur.fetchall()`|모든 조회 행 가져오기|
|`DictCursor`|결과 행을 딕셔너리로 반환|

### ⭐ 한 줄 정리

> **PyMySQL은 Connection과 Cursor를 통해 Python에서 MySQL SQL을 실행하고 결과를 가져온다.**

### 🔖 복습할 내용

- [ ] Connection과 Cursor의 역할 구분하기
- [ ] `with`문으로 연결 자원 관리하기
- [ ] 조회 결과를 DataFrame으로 변환하기
