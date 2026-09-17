---
source:
  - "[[02 정리노트/week01/day01_08.06]]"
---

# PowerShell 실행 정책

## 1. 개념

PowerShell 실행 정책은 PowerShell에서 스크립트를 실행할 수 있는 조건을 제어하는 설정이다. 현재 정책을 먼저 조회하고 필요한 정책으로 변경한 뒤 다시 조회하여 적용 여부를 확인한다.

> **핵심:** 실행 정책은 스크립트 실행 조건을 제어하며 변경 전후의 값을 조회해 확인해야 한다.

---

## 2. 쉽게 이해하기

실행 정책은 PowerShell 스크립트를 실행할 때 확인하는 통과 기준과 같다. 설정을 바꿀 때는 현재 상태를 확인하고 변경한 뒤 결과를 다시 확인하는 순서가 중요하다.

```text
현재 실행 정책 조회
  ↓
RemoteSigned로 변경
  ↓
변경 확인 메시지에 응답
  ↓
실행 정책 다시 조회
```

---

## 3. 사용 방법

관리자 권한으로 PowerShell을 열고 다음 명령을 순서대로 실행한다.

```powershell
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned
Get-ExecutionPolicy
```

- `Get-ExecutionPolicy` → 현재 실행 정책을 조회한다.
- `Set-ExecutionPolicy RemoteSigned` → 실행 정책을 `RemoteSigned`로 변경한다.
- `Y` → 변경 여부를 묻는 메시지에서 변경에 동의한다.

---

## 4. 예제

```powershell
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned
Get-ExecutionPolicy
```

마지막 조회 결과:

```text
RemoteSigned
```

마지막에 `RemoteSigned`가 출력되면 정책 변경이 적용된 것이다.

---

## 5. 헷갈리는 개념 비교

|구분|조회|변경|
|---|---|---|
|명령|`Get-ExecutionPolicy`|`Set-ExecutionPolicy RemoteSigned`|
|역할|현재 정책 확인|실행 정책 값 설정|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`실행 정책`|PowerShell 스크립트의 실행 조건을 제어하는 설정|
|`RemoteSigned`|수업에서 지정한 PowerShell 실행 정책 값|

### 💻 주요 코드

|코드|의미|
|---|---|
|`Get-ExecutionPolicy`|현재 실행 정책 조회|
|`Set-ExecutionPolicy RemoteSigned`|실행 정책 변경|

### ⭐ 한 줄 정리

> **PowerShell 실행 정책을 변경할 때는 변경 전후의 값을 조회하여 실제 적용 여부를 확인한다.**

### 🔖 복습할 내용

- [ ] PowerShell 실행 정책의 역할 설명하기
- [ ] 실행 정책 변경 명령 기억하기
- [ ] 설정 변경 후 검증하기
