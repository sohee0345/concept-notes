# MySQL · Docker · DBeaver

## 1. 개념

MySQL은 관계형 데이터베이스 관리 시스템이고, Docker Compose를 이용하면 로컬에 직접 설치하지 않고 컨테이너로 실행할 수 있다.

DBeaver는 MySQL에 접속해 SQL을 작성·실행하고 데이터를 확인하는 GUI 프로그램이다.

> **핵심:** Docker로 MySQL 서버를 실행하고 DBeaver로 접속해 SQL을 실행할 수 있다.

---

## 2. 쉽게 이해하기

전체 흐름은 `Docker로 MySQL 실행 → DBeaver로 접속 → SQL 실행`으로 생각하면 된다.

```text
docker-compose up -d
        ↓
MySQL 서버 실행
        ↓
DBeaver Connection
        ↓
SQL 실행
```

---

## 3. 사용 방법

```bash
docker-compose up -d
docker-compose down
```

```sql
SHOW TABLES;
```

- `up -d` → 컨테이너 생성 및 백그라운드 실행
- `down` → 컨테이너 중지 및 삭제
- `SHOW TABLES` → 현재 DB의 테이블 목록 확인
- DBeaver에서 SQL 실행 → `Ctrl + Enter`

---

## 4. 예제

```bash
docker-compose up -d
```

MySQL 컨테이너가 실행된 뒤 DBeaver에서 MySQL Connection을 만들고 접속한다.

접속 오류가 있을 때는 필요에 따라 `allowPublicKeyRetrieval` 설정을 확인한다.

---

## 5. 헷갈리는 개념 비교

| 구분 | Docker | DBeaver |
|---|---|---|
| 역할 | MySQL 서버 실행 환경 | MySQL 접속·SQL 실행 도구 |
| 형태 | 컨테이너 | GUI 프로그램 |
| 핵심 | 서버를 띄움 | 서버에 접속함 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- Docker Compose → 컨테이너 실행·관리
- DBeaver → DB 접속 및 SQL 실행
- MySQL → 데이터를 저장·조회하는 데이터베이스 시스템

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `docker-compose up -d` | MySQL 컨테이너 실행 |
| `docker-compose down` | 컨테이너 중지·삭제 |
| `SHOW TABLES;` | 테이블 목록 확인 |

### ⭐ 한 줄 정리

> **Docker로 MySQL 서버를 실행하고 DBeaver로 접속해 SQL을 실행할 수 있다.**

### 🔖 복습할 내용

- [ ] Docker와 DBeaver의 역할 차이
- [ ] `up -d`와 `down` 차이
- [ ] DBeaver에서 SQL 실행 방법
