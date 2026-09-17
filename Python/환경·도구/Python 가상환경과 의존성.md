---
source:
  - "[[02 정리노트/week01/day02_08.07]]"
---

# Python 가상환경과 의존성

## 1. 개념

Python 가상환경은 프로젝트마다 Python과 패키지 구성을 분리하는 공간이다. 프로젝트별 `.venv`를 만들고 필요한 패키지를 의존성 파일에 기록하면 같은 환경을 다시 구성할 수 있다.

> **핵심:** 프로젝트마다 가상환경을 분리하고 의존성을 파일에 기록하여 패키지 충돌을 줄인다.

---

## 2. 쉽게 이해하기

프로젝트마다 전용 상자를 만들어 필요한 Python과 패키지를 따로 담아 두는 것이 가상환경이다.

```text
프로젝트 폴더
  ↓
.venv 생성과 활성화
  ↓
의존성 파일 기준 패키지 설치
  ↓
작업 후 비활성화
```

---

## 3. 사용 방법

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r .\requirements.txt
deactivate
```

- `py -m venv .venv` → `.venv` 가상환경을 만든다.
- `Activate.ps1` → PowerShell에서 가상환경을 활성화한다.
- `requirements.txt` → 설치할 패키지 이름을 기록한다.
- `pip install -r` → 파일에 기록된 패키지를 설치한다.
- `deactivate` → 현재 가상환경을 비활성화한다.

---

## 4. 예제

```text
jupyter
pandas
seaborn
```

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
py -m pip install --upgrade pip
pip install -r .\requirements.txt
deactivate
```

`requirements.txt`의 패키지가 `.venv`에 설치되어 프로젝트 전용 환경이 구성된다.

---

## 5. 헷갈리는 개념 비교

|구분|venv와 pip|uv|
|---|---|---|
|환경 생성|`py -m venv .venv`|`uv init`, `uv sync`|
|의존성 기록|`requirements.txt`|`pyproject.toml`|
|패키지 설치|`pip install -r`|`uv add`, `uv sync`|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`가상환경`|프로젝트별 Python과 패키지를 분리하는 환경|
|`.venv`|프로젝트 안에 만든 가상환경 폴더|
|`의존성`|프로젝트 실행에 필요한 외부 패키지|

### 💻 주요 코드

|코드|의미|
|---|---|
|`py -m venv .venv`|가상환경 생성|
|`.\.venv\Scripts\Activate.ps1`|가상환경 활성화|
|`pip install -r requirements.txt`|기록된 의존성 설치|
|`deactivate`|가상환경 비활성화|

### ⭐ 한 줄 정리

> **가상환경은 프로젝트별 Python과 패키지를 분리하고 의존성 파일로 같은 환경을 다시 구성하게 한다.**

### 🔖 복습할 내용

- [ ] 가상환경이 필요한 이유 설명하기
- [ ] 생성·활성화·비활성화 흐름 기억하기
- [ ] venv 방식과 uv 방식 비교하기
