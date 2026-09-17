---
source:
  - "[[02 정리노트/week01/day02_08.07]]"
---

# Git 저장 공간

## 1. 개념

Git은 파일 상태를 Working Directory, Staging Area, Repository의 세 공간으로 나누어 관리한다. 작업한 모든 변경을 바로 기록하지 않고 다음 커밋에 포함할 변경을 먼저 선택한 뒤 이력으로 남긴다.

> **핵심:** 작업한 파일은 `git add`를 거쳐 Staging Area로 이동하고 `git commit`으로 Repository의 이력이 된다.

---

## 2. 쉽게 이해하기

Working Directory는 실제 작업 책상, Staging Area는 기록할 자료를 고르는 바구니, Repository는 선택한 자료를 보관하는 기록 저장소와 같다.

```text
Working Directory
  ↓ git add
Staging Area
  ↓ git commit
Repository(.git)
```

---

## 3. 사용 방법

- `Working Directory` → 프로젝트 파일을 만들고 수정하는 실제 작업 공간이다.
- `git add` → 변경을 다음 커밋 대상으로 선택한다.
- `Staging Area` → 다음 커밋에 포함할 변경을 임시로 모아 둔다.
- `git commit` → 선택된 변경을 로컬 저장소의 이력으로 기록한다.
- `.git` → 커밋 이력과 저장소 정보가 보관되는 디렉터리이다.

---

## 4. 예제

```text
파일 수정 → Modified
  ↓ git add
변경 선택 → Staged
  ↓ git commit
이력 저장 → Committed
```

`git add`는 기록할 변경을 고르고 `git commit`은 선택된 변경을 하나의 이력으로 저장한다.

---

## 5. 헷갈리는 개념 비교

|구분|Working Directory|Staging Area|Repository|
|---|---|---|---|
|의미|실제 작업 공간|커밋 대상을 고르는 공간|커밋 이력 저장 공간|
|상태|Modified|Staged|Committed|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`Working Directory`|실제 파일을 생성하고 수정하는 공간|
|`Staging Area`|다음 커밋에 포함할 변경을 선택하는 공간|
|`Repository`|커밋 이력이 저장되는 공간|

### 💻 주요 코드

|코드|의미|
|---|---|
|`git add`|변경을 Staging Area에 추가|
|`git commit`|Stage된 변경을 로컬 이력으로 저장|

### ⭐ 한 줄 정리

> **Git은 작업한 변경을 Stage에서 선택한 뒤 Commit으로 로컬 저장소의 이력에 기록한다.**

### 🔖 복습할 내용

- [ ] Git의 세 저장 공간 설명하기
- [ ] Modified, Staged, Committed 상태 구분하기
- [ ] `git add`와 `git commit`의 역할 구분하기
