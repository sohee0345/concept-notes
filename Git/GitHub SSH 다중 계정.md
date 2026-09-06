# GitHub SSH 다중 계정

## 1. 개념

SSH Key는 컴퓨터가 GitHub에 접근할 수 있음을 증명한다. 여러 GitHub 계정을 사용할 때는 SSH Profile과 Alias로 사용할 계정을 구분할 수 있다.

> **핵심:** 계정별 SSH 설정과 Alias를 구분하면 원하는 계정으로 저장소에 접근할 수 있다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
SSH Key 등록
  ↓
계정별 SSH Profile 생성
  ↓
사용할 Profile Apply
  ↓
SSH 주소의 Host를 Alias로 변경
  ↓
Private Repository Clone
```

> **쉽게 말하면:** SSH Profile은 사용할 GitHub 계정을 고르는 설정이고 Alias는 Clone 주소에 적는 계정별 별명이다.

------------------------------------------------------------------------

## 3. 사용 방법

GitHub에서 SSH Key를 등록한다.

``` text
Settings → SSH and GPG keys → New SSH key
```

VSCode에서 Profile을 만든다.

``` text
Ctrl + Shift + P
→ SSH Profiles: Open Manager
→ Create Profile
```

- `Profile Name` → GitHub 아이디
- `Provider` → GitHub
- `Description` → 계정 용도를 구분하는 설명

> **핵심:** Clone 전에 저장소에 접근할 계정의 Profile을 Apply한다.

------------------------------------------------------------------------

## 4. 예제

기본 SSH 주소:

``` text
git@github.com:sohee0345/test_github.git
```

Alias 적용 주소:

``` text
git@github.com-sohee0345:sohee0345/test_github.git
```

### 코드 해석

- `github.com` → 기본 Host
- `github.com-sohee0345` → 계정을 구분하도록 설정한 Alias
- 콜론 뒤 경로 → GitHub 소유자와 저장소 이름

> **결과 해석:** Alias가 연결된 SSH 설정을 통해 지정한 계정으로 저장소에 접근한다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | SSH Key | SSH Profile | SSH Alias |
| --- | --- | --- | --- |
| 역할 | 컴퓨터 인증 | 사용할 계정 설정 구분 | SSH 주소의 계정별 Host 구분 |
| 설정 위치 | GitHub Settings | VSCode Profile Manager | SSH 설정과 Clone 주소 |

------------------------------------------------------------------------

## 6. 주의할 점

- 여러 계정을 사용할 때 Windows 자격 증명 관리자에 남은 기존 GitHub 로그인 정보를 확인한다.
- Profile의 `Provider`는 GitHub로 지정한다.
- Clone 주소를 변경할 때 콜론 앞 Host 부분만 설정한 Alias로 바꾼다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `SSH Key` | GitHub 접근을 위한 컴퓨터 인증 수단 |
| `SSH Profile` | 여러 GitHub 계정을 구분하는 설정 |
| `SSH Alias` | 계정별 SSH Host 이름 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `git@github.com:계정/저장소.git` | 기본 SSH Clone 주소 |
| `git@Alias:계정/저장소.git` | Alias를 적용한 SSH Clone 주소 |

### ⭐ 한 줄 정리

> **SSH Key로 인증하고 Profile과 Alias로 계정을 구분해 원하는 GitHub 계정으로 Clone한다.**

### 🔖 복습할 내용

- [ ] GitHub에 SSH Key 등록하는 경로 기억하기
- [ ] VSCode에서 SSH Profile 생성하고 Apply하기
- [ ] 기본 SSH 주소를 Alias 주소로 바꾸기
