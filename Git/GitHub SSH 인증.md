---
source:
  - "[[02 정리노트/week05/day17_08.31]]"
---

# GitHub SSH 인증

## 1. 개념

SSH 인증은 공개키를 GitHub 계정에 등록하여 로컬 컴퓨터의 저장소 접근 권한을 확인하는 방식이다. 여러 계정은 SSH Profile과 Host Alias로 구분할 수 있다.

> **핵심:** 계정별 공개키, SSH Profile, Host Alias를 올바르게 연결해야 원하는 GitHub 계정으로 접근한다.

---

## 2. 쉽게 이해하기

공개키는 GitHub에 등록한 출입 명단이고 Host Alias는 여러 계정 중 사용할 출입구를 구분하는 별칭이다.

```text
SSH 키 생성·등록 → 계정별 Profile → Host Alias → SSH 주소로 Clone
```

---

## 3. 사용 방법

```text
기본 주소: git@github.com:owner/repo.git
Alias 주소: git@github.com-account:owner/repo.git
```

- GitHub의 `SSH and GPG keys`에 공개키를 등록한다.
- 계정별 SSH Profile과 Host Alias를 만든다.
- Clone 주소의 호스트를 Alias로 바꿔 사용할 계정을 지정한다.

---

## 4. 예제

VSCode 명령 팔레트에서 `Git: Clone`을 실행하고 Alias가 적용된 SSH 주소를 입력하면 해당 Profile의 계정으로 저장소에 접근한다.

---

## 5. 헷갈리는 개념 비교

|구분|공개키|Host Alias|
|---|---|---|
|역할|컴퓨터 접근 권한 인증|사용할 계정·설정 구분|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|SSH 공개키|로컬 컴퓨터의 접근 권한을 확인하는 키|
|Profile|계정별 SSH 설정 묶음|
|Host Alias|SSH 연결 설정을 구분하는 호스트 별칭|

### ⭐ 한 줄 정리

> **GitHub SSH 인증은 공개키와 Host Alias를 계정별로 연결해 저장소 접근 계정을 구분한다.**

### 🔖 복습할 내용

- [ ] 공개키 등록 흐름 설명하기
- [ ] Host Alias의 역할 설명하기
- [ ] Alias가 적용된 Clone 주소 작성하기
