# Python 가상환경과 의존성

## 1. 개념

Python 가상환경은 프로젝트별로 Python 라이브러리를 분리해 관리하는 환경이다. 의존성은 프로젝트 실행에 필요한 `jupyter`, `pandas`, `seaborn` 같은 패키지를 뜻한다.

> **핵심:** 프로젝트마다 가상환경과 의존성을 분리하면 서로 다른 프로젝트의 패키지 구성이 섞이지 않는다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
프로젝트 1 → 전용 가상환경 → 필요한 패키지 목록
프로젝트 2 → 전용 가상환경 → 별도의 패키지 목록
```

> **쉽게 말하면:** 각 프로젝트에 전용 도구 상자를 하나씩 두고, 그 프로젝트에 필요한 도구만 담아 사용하는 방식이다.

------------------------------------------------------------------------

## 3. 사용 방법

### venv와 pip 방식

``` powershell
py -m venv .venv
.\.venv\Scripts\activate
py -m pip install --upgrade pip
pip install -r .\requirements.txt
deactivate
```

`requirements.txt` 예시:

``` text
jupyter
pandas
seaborn
```

### uv 방식

``` powershell
uv init --name venv-uv --python 3.12
uv add jupyter pandas seaborn
.\.venv\Scripts\activate
deactivate
uv sync
```

- `activate` → 가상환경 활성화
- `deactivate` → 가상환경 비활성화
- `requirements.txt` → pip로 설치할 패키지 목록
- `pyproject.toml` → uv 프로젝트의 의존성을 확인한 파일

> **핵심:** 가상환경을 활성화한 뒤 패키지를 설치하고, 프로젝트의 의존성 파일에서 필요한 패키지를 확인한다.

------------------------------------------------------------------------

## 4. 예제

``` powershell
py -m venv .venv
.\.venv\Scripts\activate
pip install -r .\requirements.txt
deactivate
```

### 코드 해석

- `py -m venv .venv` → `.venv` 폴더에 가상환경을 만든다.
- `-m` → Python 모듈을 스크립트처럼 실행한다.
- `pip install -r` → 지정한 파일에 적힌 패키지를 설치한다.
- `deactivate` → 현재 가상환경 사용을 종료한다.

> **결과 해석:** `.venv` 안에 프로젝트 전용 환경이 만들어지고, `requirements.txt`의 패키지가 그 환경에 설치된다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | venv와 pip | uv |
| --- | --- | --- |
| 환경 생성 | `py -m venv .venv` | `uv init --python 3.12` |
| 의존성 추가 | `requirements.txt` 작성 후 `pip install -r` | `uv add` |
| 의존성 확인 | `requirements.txt` | `pyproject.toml` |
| 환경 복구·동기화 | 목록을 이용해 다시 설치 | `uv sync` |

------------------------------------------------------------------------

## 6. 주의할 점

- `-m`은 관리자 모드가 아니라 Python 모듈을 실행하는 옵션이다.
- VSCode는 가상환경을 만들 프로젝트 폴더 단위로 연다.
- 패키지 설치 전 현재 가상환경이 활성화되었는지 확인한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `가상환경` | 프로젝트별로 분리한 Python 실행 환경 |
| `의존성` | 프로젝트 실행에 필요한 패키지 |
| `.venv` | 수업에서 사용한 가상환경 폴더 이름 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `py -m venv .venv` | venv 가상환경 생성 |
| `pip install -r requirements.txt` | 패키지 목록 설치 |
| `uv add` | uv 프로젝트에 의존성 추가 |
| `uv sync` | uv 프로젝트 환경 동기화 |

### ⭐ 한 줄 정리

> **Python 가상환경은 프로젝트마다 필요한 패키지를 독립적으로 설치하고 의존성 파일로 관리하게 해 준다.**

### 🔖 복습할 내용

- [ ] 가상환경 생성과 활성화 순서 기억하기
- [ ] `requirements.txt`와 `pyproject.toml` 비교하기
- [ ] `-m` 옵션의 정확한 의미 설명하기
