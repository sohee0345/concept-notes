# Git 저장 공간과 기본 흐름

## 1. 개념

Git은 파일의 변경 내용을 Working Directory, Staging Area, Repository라는 세 공간으로 나누어 관리한다. 변경한 파일을 선택하고 Commit하기까지 각 공간을 순서대로 거친다.

> **핵심:** 파일 수정은 Working Directory에서 시작하며, `git add`와 `git commit`을 거쳐 저장소 이력이 된다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
Working Directory
파일을 만들고 수정하는 작업대
  ↓ git add
Staging Area
이번에 저장할 파일을 고르는 준비 공간
  ↓ git commit
Repository (.git)
선택한 변경 내용을 이력으로 보관하는 공간
```

> **쉽게 말하면:** 작업한 파일 중 저장할 것을 장바구니에 담고, Commit으로 구매 내역처럼 기록을 확정하는 과정이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` text
파일 수정 → Modified
git add → Staged
git commit → Committed
```

- `Working Directory` → 실제 프로젝트 파일이 있는 공간
- `Staging Area` → 다음 Commit에 넣을 변경을 모으는 공간
- `Repository` → Commit 이력이 `.git` 디렉터리에 저장되는 공간
- `Changes` → 아직 Stage하지 않은 변경 파일
- `Staged Changes` → 다음 Commit에 포함할 파일

> **핵심:** 모든 변경을 바로 Commit하는 것이 아니라 Staging Area에서 Commit할 파일을 먼저 선택한다.

------------------------------------------------------------------------

## 4. 예제

``` text
sample 폴더 또는 파일 생성
  ↓
Working Directory에서 Changes 확인
  ↓ git add
Staged Changes로 이동
  ↓ git commit
Git Graph에서 Commit 기록 확인
```

### 코드 해석

- `git add` → 변경 파일을 Staging Area에 올린다.
- `git commit` → Staged 상태의 변경을 Repository 이력으로 기록한다.

> **결과 해석:** Commit이 완료되면 Git Graph에서 새로운 Commit 기록을 확인할 수 있다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | Working Directory | Staging Area | Repository |
| --- | --- | --- | --- |
| 역할 | 파일 생성·수정 | Commit 대상 선택 | 변경 이력 저장 |
| 상태 | Modified | Staged | Committed |
| 이동 명령 | 작업 시작점 | `git add` | `git commit` |

------------------------------------------------------------------------

## 6. 주의할 점

- `Changes`에 있는 파일은 아직 다음 Commit 대상으로 선택되지 않은 상태이다.
- 프로젝트의 `.git` 폴더에는 Git 저장소의 이력이 보관되므로 일반 작업 파일과 역할이 다르다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `Modified` | Working Directory에서 파일이 변경된 상태 |
| `Staged` | 다음 Commit 대상으로 선택된 상태 |
| `Committed` | 변경 내용이 저장소 이력으로 기록된 상태 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `git add` | 변경 파일을 Staging Area에 추가 |
| `git commit` | Staged 변경을 Repository에 기록 |

### ⭐ 한 줄 정리

> **Git의 변경 내용은 Working Directory에서 시작해 Staging Area를 거쳐 Repository의 Commit 이력으로 저장된다.**

### 🔖 복습할 내용

- [ ] Git의 세 저장 공간 설명하기
- [ ] Modified, Staged, Committed 상태 구분하기
- [ ] `git add`와 `git commit`의 역할 비교하기
