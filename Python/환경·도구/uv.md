---
source:
  - "[[02 정리노트/week01/day01_08.06]]"
  - "[[02 정리노트/week01/day02_08.07]]"
---

# uv

## 1. 개념

`uv`는 Python 버전과 프로젝트 의존성을 관리하는 도구이다. 필요한 Python 버전을 설치하고, 프로젝트를 초기화한 뒤 패키지를 추가하거나 설정에 맞게 가상환경을 동기화할 수 있다.

> **핵심:** uv는 Python 버전 설치부터 프로젝트 의존성 기록과 가상환경 동기화까지 관리한다.

---

## 2. 쉽게 이해하기

프로젝트마다 필요한 Python 버전과 패키지가 다를 수 있다. uv는 프로젝트 설정에 사용할 Python과 패키지를 기록하여 같은 환경을 다시 구성하도록 도와준다.

```text
uv 설치 확인
  ↓
Python 버전 목록 조회
  ↓
필요한 버전 설치
  ↓
프로젝트 초기화와 의존성 추가
  ↓
가상환경 동기화
```

---

## 3. 사용 방법

```powershell
uv --version
uv python list
uv python install 3.12
uv init --name venv-uv --python 3.12
uv add jupyter pandas seaborn
uv sync
```

- `uv --version` → uv가 정상적으로 설치되었는지 확인한다.
- `uv python list` → 사용할 수 있거나 설치된 Python 버전을 확인한다.
- `uv python install 3.12` → Python 3.12를 설치한다.
- `uv init` → uv 프로젝트를 초기화하고 Python 버전을 지정한다.
- `uv add` → 패키지를 프로젝트 의존성에 추가하고 설치한다.
- `uv sync` → 프로젝트 설정에 맞게 가상환경과 패키지를 맞춘다.
- `pyproject.toml` → 프로젝트 정보와 의존성을 기록한다.

---

## 4. 예제

```powershell
uv init --name venv-uv --python 3.12
uv add jupyter pandas seaborn
uv sync
```

Python 3.12를 사용하는 프로젝트를 초기화하고 세 패키지를 의존성에 추가한다. `uv sync`는 프로젝트 설정을 기준으로 가상환경과 패키지 구성을 맞춘다.

---

## 5. 헷갈리는 개념 비교

|구분|`uv add`|`uv sync`|
|---|---|---|
|역할|의존성 추가와 설치|설정과 가상환경 동기화|
|사용|새 패키지가 필요할 때|기록된 환경을 다시 구성할 때|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`uv`|Python 버전과 프로젝트 의존성을 관리하는 도구|
|`pyproject.toml`|프로젝트 정보와 의존성을 기록하는 파일|

### 💻 주요 코드

|코드|의미|
|---|---|
|`uv --version`|uv 설치 버전 확인|
|`uv python list`|Python 버전 목록 확인|
|`uv python install 3.12`|Python 3.12 설치|
|`uv add 패키지명`|프로젝트 의존성 추가|
|`uv sync`|설정과 가상환경 동기화|

### ⭐ 한 줄 정리

> **uv는 Python 버전과 프로젝트 의존성을 기록하고 가상환경을 설정에 맞게 동기화하는 도구이다.**

### 🔖 복습할 내용

- [ ] uv의 역할 설명하기
- [ ] `uv add`와 `uv sync`의 역할 구분하기
- [ ] `pyproject.toml`에 기록되는 내용 설명하기
