# GitHub 자격 증명 · Branch Protection

## 1. 개념

Windows에서는 GitHub 인증 정보를 자격 증명 관리자에서 확인할 수 있다.

GitHub의 Branch Protection Rule은 `main` 같은 중요한 브랜치를 실수로 수정하거나 삭제하지 못하도록 보호하는 설정이다.

> **핵심:** GitHub에서는 인증 정보를 관리하고 중요한 브랜치를 보호하여 안전하게 협업할 수 있다.

---

## 2. 쉽게 이해하기

브랜치를 작업 단계별 공간이라고 생각하면 쉽다.

```text
main → 안정된 최종 코드
dev  → 개발 중인 코드 통합·테스트
```

---

## 3. 사용 방법

```text
제어판
→ 자격 증명 관리자
→ Windows 자격 증명
→ GitHub 관련 정보 확인
```

```text
Repository
→ Settings
→ Branches
→ Branch Protection Rule
```

---

## 4. 예제

`main`을 보호하고 실제 개발은 `dev`나 `feature` 브랜치에서 진행하는 식으로 운영할 수 있다.

---

## 5. 헷갈리는 개념 비교

| 브랜치 | 역할 |
|---|---|
| `main` | 안정된 최종 코드 |
| `dev` | 개발 중인 코드 통합·테스트 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- 자격 증명 관리자 → GitHub 로그인 정보 관리
- Branch Protection Rule → 중요 브랜치 보호
- main/dev 분리 → 안정성과 개발 흐름 분리

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `main` | 안정된 최종 브랜치 |
| `dev` | 개발 통합 브랜치 |

### ⭐ 한 줄 정리

> **GitHub에서는 인증 정보를 관리하고 중요한 브랜치를 보호하여 안전하게 협업할 수 있다.**

### 🔖 복습할 내용

- [ ] Windows 자격 증명 관리자 위치
- [ ] main과 dev 역할 차이
- [ ] Branch Protection Rule 목적
