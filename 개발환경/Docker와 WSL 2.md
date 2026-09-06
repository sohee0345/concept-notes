# Docker와 WSL 2

## 1. 개념

WSL은 Windows에서 Linux 바이너리를 실행할 수 있게 해 주는 Windows Subsystem for Linux이다. 수업에서는 WSL 2를 준비한 뒤 Windows용 Docker를 설치하고, 실행 오류가 발생했을 때 WSL을 점검하고 업데이트했다.

> **핵심:** Windows에서 Docker 실행에 문제가 생기면 WSL 2의 설치 여부와 버전, Windows 기능 활성화 상태를 함께 확인한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

WSL 2는 Windows 안에서 Linux 환경을 사용할 수 있도록 준비해 주며, 수업에서는 Docker가 이 환경과 함께 정상적으로 동작하도록 설치와 설정을 진행했다.

``` text
WSL 설치
  ↓
컴퓨터 재부팅
  ↓
WSL 버전 확인 및 기본 버전을 2로 설정
  ↓
Windows용 Docker 설치
  ↓
오류 발생 시 WSL 업데이트와 Windows 기능 점검
```

> **쉽게 말하면:** Docker가 Windows에서 사용할 Linux 환경을 WSL 2로 준비하고, 문제가 생기면 그 연결 환경부터 확인하는 과정이다.

------------------------------------------------------------------------

## 3. 사용 방법

관리자 권한으로 Windows PowerShell을 열고 WSL을 설치한다.

``` powershell
wsl --install
```

설치 후 컴퓨터를 재부팅하고 다음 명령을 실행한다.

``` powershell
wsl --version
wsl --set-default-version 2
```

- `wsl --install` → WSL 설치
- `wsl --version` → WSL 버전 확인
- `wsl --set-default-version 2` → 새 Linux 배포판에 사용할 기본 WSL 버전을 2로 설정

> **핵심:** WSL 설치 후 재부팅하고, 버전 확인과 기본 버전 설정을 진행한다.

------------------------------------------------------------------------

## 4. Docker 오류 점검 예제

Docker 설치 후 오류가 발생하면 먼저 WSL을 업데이트한다.

``` powershell
wsl --update
```

Windows 기능도 다음 순서로 확인한다.

``` text
제어판
  ↓
프로그램 → 프로그램 및 기능
  ↓
Windows 기능 켜기/끄기
  ↓
Linux용 Windows 하위 시스템 체크
  ↓
확인 → 재부팅
```

필요하면 WSL 업데이트와 설치 명령을 다시 실행한 뒤 재부팅한다.

``` powershell
wsl --update
wsl --install
```

### 코드 해석

- `wsl --update` → WSL을 최신 버전으로 업데이트한다.
- `wsl --install` → WSL 설치를 진행한다.
- Windows 기능의 `Linux용 Windows 하위 시스템` → WSL 사용에 필요한 Windows 기능이다.

> **결과 해석:** WSL을 업데이트하고 필요한 Windows 기능을 활성화한 뒤 재부팅하여 Docker 오류가 해결되었는지 확인한다.

------------------------------------------------------------------------

## 5. Docker Compose로 MySQL 실행

Docker Compose는 `docker-compose.yml`에 작성된 설정을 기준으로 컨테이너를 생성하고 실행한다. 수업에서는 PC에 MySQL을 직접 설치하지 않고 MySQL 서버 컨테이너를 실행했다.

``` text
docker-compose.yml
  ↓
docker compose up -d
  ↓
MySQL 컨테이너 생성·실행
  ↓
Docker Desktop에서 Running 상태 확인
```

``` powershell
docker compose up -d
docker compose down
```

- `docker-compose.yml` → MySQL 이미지 버전, 포트, 계정, 비밀번호, 데이터베이스 이름 등의 설정 정의
- `docker compose up -d` → 설정을 읽어 컨테이너를 생성하고 백그라운드에서 실행
- `docker compose down` → Compose로 만든 컨테이너를 중지하고 제거
- `-d` → 터미널을 계속 점유하지 않는 백그라운드 실행

실행 후 Docker Desktop에서 컨테이너가 Running 상태인지 확인한다.

![[04 실습파일/week03/day09/스크린샷 2026-08-19 124816.png]]

> **핵심:** 설정 파일로 MySQL 실행 환경을 정의하고 `up -d`로 실행한 뒤 Docker Desktop에서 상태를 검증한다.

------------------------------------------------------------------------

## 6. 헷갈리는 개념 비교

| 구분 | WSL 2 | Docker | Docker Compose |
| --- | --- | --- | --- |
| 의미 | Windows에서 Linux 바이너리를 실행할 수 있게 해 주는 하위 시스템 | 컨테이너 실행 환경 | 설정 파일로 컨테이너 구성 관리 |
| 확인 | `wsl --version` | Docker Desktop 실행 화면 | 컨테이너 Running 상태 |
| 주요 명령 | `wsl --update` | Docker Desktop에서 상태 확인 | `docker compose up -d` |

------------------------------------------------------------------------

## 7. 주의할 점

- `wsl --install` 실행 후에는 수업 절차에 따라 컴퓨터를 재부팅한다.
- `wsl --set-default-version 2`를 실행해 기본 WSL 버전을 2로 설정한다.
- Docker 오류 해결 과정에서 Windows 기능을 변경했다면 재부팅 후 결과를 확인한다.
- `docker compose down`은 Compose로 실행한 컨테이너를 중지하고 제거하므로 대상 프로젝트를 확인한다.
- MySQL을 실행한 뒤 Docker Desktop에서 컨테이너 상태가 Running인지 확인한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `WSL` | Windows에서 Linux 바이너리를 실행할 수 있게 해 주는 하위 시스템 |
| `WSL 2` | 수업에서 Docker 환경을 위해 기본값으로 설정한 WSL 버전 |
| `Docker 오류 점검` | WSL 업데이트와 Windows 기능 활성화 상태를 확인하는 과정 |
| `Docker Compose` | 설정 파일을 기준으로 컨테이너를 실행·정리하는 기능 |
| `docker-compose.yml` | MySQL 컨테이너의 실행 설정을 정의하는 파일 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `wsl --install` | WSL 설치 |
| `wsl --version` | WSL 버전 확인 |
| `wsl --set-default-version 2` | 기본 WSL 버전을 2로 설정 |
| `wsl --update` | WSL 업데이트 |
| `docker compose up -d` | 컨테이너 생성 및 백그라운드 실행 |
| `docker compose down` | 컨테이너 중지 및 제거 |

### ⭐ 한 줄 정리

> **Windows에서 WSL 2 기반 Docker 환경을 준비하고 Docker Compose 설정으로 MySQL 같은 컨테이너를 실행·관리한다.**

### 🔖 복습할 내용

- [ ] WSL 설치 후 필요한 작업 확인하기
- [ ] 기본 WSL 버전을 2로 설정하는 명령 기억하기
- [ ] Docker 오류 발생 시 WSL과 Windows 기능 점검 순서 복습하기
- [ ] `docker-compose.yml`과 Compose 명령의 관계 설명하기
- [ ] MySQL 컨테이너를 실행하고 Running 상태 확인하기
- [ ] `docker compose up -d`와 `down` 비교하기
