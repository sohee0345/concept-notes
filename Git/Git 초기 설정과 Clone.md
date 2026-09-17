---
source:
  - "[[02 정리노트/week01/day01_08.06]]"
---

# Git 초기 설정과 Clone

## 1. 개념

Git은 파일의 변경 이력을 관리하고 원격 저장소와 협업할 때 사용하는 버전 관리 도구이다. 설치 후에는 커밋 작성자를 구분할 사용자 이름과 이메일을 등록하며, 원격 저장소를 로컬 컴퓨터로 복제하는 작업을 `clone`이라고 한다.

> **핵심:** Git을 설치한 뒤 작성자 정보를 설정하고, Clone으로 원격 저장소를 로컬에 복제한다.

---

## 2. 쉽게 이해하기

Git 사용자 정보는 변경 기록을 남긴 사람을 구분하는 서명과 비슷하다. Clone은 GitHub에 있는 프로젝트와 변경 이력을 내 컴퓨터로 내려받아 작업을 시작하는 과정이다.

```text
Git 설치
  ↓
사용자 이름과 이메일 등록
  ↓
원격 저장소 주소 복사
  ↓
로컬 컴퓨터에 Clone
```

---

## 3. 사용 방법

```powershell
git --version
git config --global user.name "GitHub 아이디"
git config --global user.email "이메일"
git config --list
```

- `git --version` → 설치된 Git 버전을 확인한다.
- `git config --global user.name` → 커밋 작성자 이름을 등록한다.
- `git config --global user.email` → 커밋 작성자 이메일을 등록한다.
- `git config --list` → 저장된 Git 설정을 확인한다.

---

## 4. 예제

```text
GitHub 저장소에서 Code 선택
  ↓
저장소 주소 복사
  ↓
VSCode에서 Ctrl+Shift+P
  ↓
Git: Clone 실행 후 주소 입력
  ↓
저장할 로컬 폴더 선택
```

`Ctrl+Shift+P`로 VSCode 명령 팔레트를 열고 `Git: Clone`을 선택하면 복사한 주소의 저장소를 로컬 컴퓨터로 내려받을 수 있다.

---

## 5. 헷갈리는 개념 비교

|구분|Git 사용자 설정|Clone|
|---|---|---|
|의미|커밋 작성자 정보 등록|원격 저장소를 로컬로 복제|
|사용|Git 설치 후 초기 설정|원격 프로젝트를 내려받을 때|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`Git`|파일의 변경 이력을 관리하는 도구|
|`사용자 설정`|커밋 작성자를 구분하기 위한 이름과 이메일 등록|
|`Clone`|원격 Git 저장소를 로컬 컴퓨터에 복제하는 작업|

### 💻 주요 코드

|코드|의미|
|---|---|
|`git --version`|Git 설치 버전 확인|
|`git config --global user.name`|작성자 이름 등록|
|`git config --global user.email`|작성자 이메일 등록|
|`git config --list`|Git 설정 확인|

### ⭐ 한 줄 정리

> **Git 작업을 시작하려면 작성자 정보를 등록하고 원격 저장소를 Clone한 뒤 설정 결과를 확인한다.**

### 🔖 복습할 내용

- [ ] Git 사용자 이름과 이메일이 필요한 이유 설명하기
- [ ] Clone의 의미 설명하기
- [ ] VSCode에서 저장소를 Clone하는 흐름 설명하기
