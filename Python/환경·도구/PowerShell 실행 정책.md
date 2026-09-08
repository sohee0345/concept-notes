# PowerShell 실행 정책

## 1. 개념

PowerShell 실행 정책은 PowerShell 스크립트를 어떤 조건에서 실행할 수 있는지 제어하는 설정이다. Windows 개발 환경을 구성할 때 현재 정책을 확인한 뒤 `RemoteSigned`로 변경할 수 있다.

> **핵심:** 실행 정책을 변경할 때는 현재 값을 먼저 확인하고 변경 후 다시 조회하여 적용 여부를 검증한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
현재 실행 정책 확인
  ↓
RemoteSigned로 변경
  ↓
정책을 다시 조회하여 검증
```

> **쉽게 말하면:** PowerShell 스크립트가 실행되어도 되는지 판단하는 기본 안전 규칙을 정하는 것이다.

------------------------------------------------------------------------

## 3. 사용 방법

관리자 권한으로 PowerShell을 열고 다음 명령을 실행한다.

``` powershell
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned
Get-ExecutionPolicy
```

- `Get-ExecutionPolicy` → 현재 실행 정책을 확인한다.
- `Set-ExecutionPolicy RemoteSigned` → 실행 정책을 `RemoteSigned`로 변경한다.
- `Y` → 정책 변경 확인 메시지에 동의한다.

> **핵심:** 설정을 바꾼 뒤 `Get-ExecutionPolicy`를 다시 실행하여 결과가 `RemoteSigned`인지 확인한다.

------------------------------------------------------------------------

## 4. 예제

``` powershell
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned
Get-ExecutionPolicy
```

마지막 명령의 실행 결과:

``` text
RemoteSigned
```

### 코드 해석

- 첫 번째 조회는 변경 전 상태를 확인한다.
- `Set-ExecutionPolicy`는 정책을 변경한다.
- 마지막 조회는 변경 결과를 검증한다.

> **결과 해석:** 마지막에 `RemoteSigned`가 출력되면 설정이 적용된 것이다.

------------------------------------------------------------------------

## 6. 주의할 점

- 설정을 변경하기 전과 후에 정책을 조회하여 실제 적용 여부를 확인한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `실행 정책` | PowerShell 스크립트의 실행 조건을 제어하는 설정 |
| `RemoteSigned` | 수업의 Windows 개발 환경에서 지정한 실행 정책 |
| `검증` | 변경 후 설정값을 다시 확인하는 과정 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `Get-ExecutionPolicy` | 현재 실행 정책 확인 |
| `Set-ExecutionPolicy RemoteSigned` | 실행 정책 변경 |

### ⭐ 한 줄 정리

> **PowerShell 실행 정책은 스크립트 실행 조건을 정하며, 변경 전후의 값을 조회해 적용 여부를 확인해야 한다.**

### 🔖 복습할 내용

- [ ] 현재 실행 정책 확인하기
- [ ] `RemoteSigned`의 의미 설명하기
- [ ] 정책 변경 후 결과 검증하기
