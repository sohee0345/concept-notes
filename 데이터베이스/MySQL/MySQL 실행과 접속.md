---
source:
  - "[[02 정리노트/week03/day09_08.19]]"
---

# MySQL 실행과 접속

## 1. 개념

MySQL 서버를 Docker 컨테이너로 실행하고 DBeaver에서 서버 주소, 포트, 사용자 정보를 입력해 접속할 수 있다. 연결 전에는 컨테이너 실행 상태와 접속 정보를 확인한다.

> **핵심:** MySQL 서버 실행과 데이터베이스 접속은 별도 단계이며 연결 테스트로 설정을 검증한다.

---

## 2. 쉽게 이해하기

Docker가 데이터베이스 서버를 실행하고 DBeaver가 그 서버에 접속해 SQL을 작성하는 작업 창을 제공한다.

```text
Docker로 MySQL 실행
  ↓
DBeaver 연결 정보 입력
  ↓ Test Connection
SQL 편집기 사용
```

---

## 3. 사용 방법

```bash
docker compose up -d
docker compose down
```

- `up -d` → 서비스를 백그라운드에서 실행한다.
- `down` → 컨테이너와 네트워크를 중지하고 제거한다.
- 로컬 MySQL은 보통 `localhost`와 포트 `3306`을 사용한다.
- DBeaver에서 `Ctrl + Enter`로 현재 SQL 문장을 실행한다.

---

## 4. 예제

```sql
SHOW DATABASES;
USE examplesdb;
SHOW TABLES;
```

서버의 데이터베이스 목록을 확인하고 사용할 데이터베이스를 선택한 뒤 테이블 목록을 조회한다.

---

## 5. 헷갈리는 개념 비교

|구분|Docker|DBeaver|
|---|---|---|
|역할|MySQL 서버 환경 실행|서버 접속과 SQL 실행|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|Docker Compose|MySQL 컨테이너 실행 관리|
|DBeaver|데이터베이스 접속과 SQL 실행 GUI|
|연결 테스트|접속 정보가 올바른지 확인하는 과정|

### 💻 주요 코드

|코드|의미|
|---|---|
|`docker compose up -d`|MySQL 서비스 실행|
|`SHOW DATABASES`|데이터베이스 목록 조회|
|`USE database`|사용할 데이터베이스 선택|

### ⭐ 한 줄 정리

> **Docker에서 MySQL 서버를 실행하고 DBeaver의 연결 테스트를 거쳐 SQL을 실행한다.**

### 🔖 복습할 내용

- [ ] 서버 실행과 접속 단계 구분하기
- [ ] 기본 Host와 Port 기억하기
- [ ] DBeaver에서 SQL 실행하기
