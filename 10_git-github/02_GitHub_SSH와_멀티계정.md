# GitHub SSH와 멀티 계정 관리

## 1. 개념

SSH Key는 내 컴퓨터가 GitHub에 접근할 수 있다는 것을 증명하는 인증 수단이다.

여러 GitHub 계정을 사용하는 경우 SSH Profile과 SSH Alias를 이용하면 어떤 계정으로 Repository에 접근할지 구분할 수 있다.

> **핵심:** SSH Key는 인증, Profile과 Alias는 여러 GitHub 계정을 구분해서 사용하기 위한 설정이다.

---

## 2. 쉽게 이해하기

여러 GitHub 계정을 사용한다고 생각해보자.

```text
내 컴퓨터
  ↓
SSH Key
  ↓
GitHub 인증

계정 A → Profile A → Alias A
계정 B → Profile B → Alias B
```

SSH Key는 신분증처럼 인증 역할을 하고, Profile과 Alias는 어떤 계정을 사용할지 구분하는 이름표라고 생각하면 쉽다.

---

## 3. 사용 방법

GitHub에서 SSH Key 등록:

```text
Settings
→ SSH and GPG keys
→ New SSH key
```

VSCode SSH Profile 생성:

```text
Ctrl + Shift + P
→ SSH Profiles: Open Manager
→ Create Profile
```

Private Repository Clone:

```text
git@github.com:username/repository.git
```

SSH Alias가 있다면 Host 부분을 변경한다.

```text
git@github.com-username:username/repository.git
```

---

## 4. 예제

기본 SSH 주소:

```text
git@github.com:sohee0345/test_github.git
```

Alias:

```text
github.com-sohee0345
```

변경 후:

```text
git@github.com-sohee0345:sohee0345/test_github.git
```

---

## 5. 헷갈리는 개념 비교

| 구분 | SSH Key | SSH Profile | SSH Alias |
|---|---|---|---|
| 의미 | GitHub 인증 수단 | 사용할 계정 설정 | SSH Host 별명 |
| 목적 | 로그인 인증 | 계정 구분 | Clone 시 계정 구분 |
| 사용 위치 | GitHub / 로컬 SSH | VSCode | SSH 설정 및 Clone URL |

---

## 🟦 핵심 정리

### 💡 주요 개념

- SSH Key → GitHub 접근 인증
- SSH Profile → 여러 GitHub 계정 구분
- SSH Alias → Clone할 계정의 Host 구분
- Windows 자격 증명 관리자 → 기존 GitHub 로그인 정보 확인

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `git@github.com:user/repo.git` | 기본 GitHub SSH 주소 |
| `git@alias:user/repo.git` | SSH Alias를 사용한 주소 |

### ⭐ 한 줄 정리

> **SSH Key로 인증하고 Profile과 Alias로 여러 GitHub 계정을 구분해서 사용할 수 있다.**

### 🔖 복습할 내용

- [ ] SSH Key와 SSH Alias 차이
- [ ] Profile을 Apply해야 하는 이유
- [ ] Clone URL에서 어느 부분을 Alias로 바꾸는지
