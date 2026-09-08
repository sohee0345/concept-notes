# WSL 2와 Docker Desktop

## 1. 개념

WSL(Windows Subsystem for Linux)은 Windows에서 Linux 실행 환경을 사용할 수 있게 하는 기능이다. Docker Desktop은 Windows에서 컨테이너를 실행할 때 WSL 2 기반 환경을 사용할 수 있으므로 WSL의 설치 상태와 버전이 중요하다.

> **핵심:** Windows에서 Docker Desktop을 사용하려면 WSL 2가 설치되어 있고 정상적으로 동작하는지 함께 확인한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
Windows
  ↓ WSL 2
Linux 실행 환경
  ↓ Docker Desktop
컨테이너 실행
```

> **쉽게 말하면:** WSL 2가 Windows 안에 Linux 기반을 마련하고, Docker Desktop이 그 기반을 이용해 컨테이너를 실행한다.

------------------------------------------------------------------------

## 3. 사용 방법

PowerShell에서 WSL을 설치하고 버전을 확인한 뒤 기본 버전을 2로 지정한다.

``` powershell
wsl --install
wsl --version
wsl --set-default-version 2
```

- `wsl --install` → WSL을 설치한다.
- `wsl --version` → 설치된 WSL의 버전을 확인한다.
- `wsl --set-default-version 2` → 새 Linux 배포판의 기본 WSL 버전을 2로 지정한다.

> **핵심:** 설치나 설정 변경 후에는 필요한 경우 컴퓨터를 재부팅하고 WSL이 정상적으로 실행되는지 확인한다.

------------------------------------------------------------------------

## 4. 예제

Docker Desktop 실행 중 WSL 관련 오류가 발생하면 다음 명령으로 WSL을 업데이트하고 설치 상태를 확인한다.

``` powershell
wsl --update
wsl --install
```

제어판의 `Windows 기능 켜기/끄기`에서 `Linux용 Windows 하위 시스템`도 활성화되어 있는지 확인한다.

### 코드 해석

- `wsl --update`는 WSL을 최신 상태로 갱신한다.
- `wsl --install`은 필요한 WSL 구성 요소를 설치한다.

> **결과 해석:** WSL이 설치되고 최신 상태이면 Docker Desktop이 컨테이너를 실행할 Linux 기반을 사용할 수 있다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | WSL 2 | Docker Desktop |
| --- | --- | --- |
| 역할 | Windows에서 Linux 실행 환경 제공 | 컨테이너 생성과 실행 관리 |
| 중심 대상 | Linux 배포판과 명령 실행 | 애플리케이션 컨테이너 |
| 관계 | Docker가 활용할 수 있는 Linux 기반 | WSL 2 기반에서 컨테이너 실행 가능 |

------------------------------------------------------------------------

## 6. 주의할 점

- `wsl --set-default-version 2`는 이후 새로 설치하는 Linux 배포판의 기본 버전을 지정하는 명령이다.
- WSL 구성 요소를 설치하거나 변경한 뒤에는 재부팅이 필요할 수 있다.
- Docker 오류가 모두 WSL 문제인 것은 아니므로 오류 메시지와 WSL 상태를 함께 확인한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `WSL` | Windows에서 Linux 환경을 실행하는 기능 |
| `WSL 2` | Windows에서 Docker가 활용할 수 있는 Linux 실행 환경 |
| `Docker Desktop` | Windows에서 컨테이너를 관리하고 실행하는 도구 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `wsl --install` | WSL 설치 |
| `wsl --version` | WSL 버전 확인 |
| `wsl --set-default-version 2` | 새 배포판의 기본 WSL 버전을 2로 지정 |
| `wsl --update` | WSL 업데이트 |

### ⭐ 한 줄 정리

> **WSL 2는 Windows에서 Linux 환경을 제공하며 Docker Desktop이 컨테이너를 실행할 기반으로 사용할 수 있다.**

### 🔖 복습할 내용

- [ ] WSL 2와 Docker Desktop의 역할 구분하기
- [ ] WSL 설치와 버전 확인하기
- [ ] Docker의 WSL 관련 오류 점검 순서 설명하기
