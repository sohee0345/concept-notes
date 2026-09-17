---
source:
  - "[[02 정리노트/week01/day01_08.06]]"
---

# WSL 2와 Docker

## 1. 개념

WSL(Windows Subsystem for Linux)은 Windows에서 Linux 실행 환경을 사용할 수 있게 하는 기능이다. Docker는 격리된 컨테이너 환경에서 프로그램을 실행하는 도구이며, Windows에서 Docker Desktop을 사용할 때는 WSL이 설치되어 있고 최신 상태인지 함께 확인한다.

> **핵심:** Windows에서 Docker를 사용하기 위한 기반으로 WSL 2를 설치하고 정상 상태를 확인한다.

---

## 2. 쉽게 이해하기

WSL 2는 Windows 안에서 Linux 환경을 사용할 수 있는 바탕을 만들고, Docker는 그 기반에서 격리된 컨테이너로 프로그램을 실행한다.

```text
WSL 설치
  ↓
기본 버전을 WSL 2로 지정
  ↓
Docker Desktop 설치
  ↓
오류 발생 시 WSL 상태 확인과 업데이트
```

---

## 3. 사용 방법

```powershell
wsl --install
wsl --version
wsl --set-default-version 2
```

- `wsl --install` → WSL을 설치한다.
- `wsl --version` → 설치된 WSL 버전을 확인한다.
- `wsl --set-default-version 2` → 새 Linux 배포판의 기본 WSL 버전을 2로 지정한다.

---

## 4. 예제

Docker Desktop 실행 중 WSL 관련 오류가 발생하면 다음 명령으로 WSL 상태를 정비한다.

```powershell
wsl --update
wsl --install
```

`wsl --update`로 WSL을 최신 상태로 만들고 설치 상태를 확인한 뒤 컴퓨터를 재부팅한다.

---

## 5. 헷갈리는 개념 비교

|구분|WSL 2|Docker|
|---|---|---|
|의미|Windows에서 Linux 실행 환경을 제공하는 기능|격리된 컨테이너에서 프로그램을 실행하는 도구|
|역할|Linux 기반 도구를 사용할 바탕 마련|프로그램을 컨테이너 단위로 실행|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`WSL 2`|Windows에서 Linux 환경을 실행할 수 있게 하는 기능|
|`Docker`|격리된 컨테이너 환경에서 프로그램을 실행하는 도구|
|`Docker Desktop`|Windows에서 사용하는 Docker 실행 환경|

### 💻 주요 코드

|코드|의미|
|---|---|
|`wsl --install`|WSL 설치|
|`wsl --version`|WSL 버전 확인|
|`wsl --set-default-version 2`|기본 WSL 버전을 2로 지정|
|`wsl --update`|WSL 업데이트|

### ⭐ 한 줄 정리

> **Windows에서 Docker를 사용하려면 WSL 2를 설치하고 최신 상태와 관련 Windows 기능을 함께 확인한다.**

### 🔖 복습할 내용

- [ ] WSL 2와 Docker의 역할 구분하기
- [ ] 기본 WSL 버전을 2로 지정하기
- [ ] Docker의 WSL 오류 발생 시 확인 순서 설명하기
