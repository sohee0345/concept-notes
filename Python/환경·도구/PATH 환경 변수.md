---
source:
  - "[[02 정리노트/week01/day01_08.06]]"
---

# PATH 환경 변수

## 1. 개념

PATH는 터미널이 실행 파일을 찾을 때 확인하는 경로 목록이다. Python 실행 경로가 PATH에 등록되어 있으면 현재 폴더와 관계없이 터미널에서 `python` 명령을 실행할 수 있다.

> **핵심:** PATH에 실행 파일의 위치를 등록하면 전체 경로를 입력하지 않고 프로그램을 실행할 수 있다.

---

## 2. 쉽게 이해하기

터미널에 `python`이라고 입력하면 컴퓨터는 PATH에 등록된 폴더를 차례로 확인하며 Python 실행 파일을 찾는다.

```text
python 명령 입력
  ↓
PATH의 경로 확인
  ↓
Python 실행 파일 발견
  ↓
명령 실행
```

---

## 3. 사용 방법

Python 설치 화면에서 `Add Python to PATH`를 선택한 뒤 다음 명령으로 정상 인식 여부를 확인한다.

```powershell
python --version
```

- `Add Python to PATH` → Python 실행 경로를 PATH에 등록한다.
- `python` → PATH에서 Python 실행 파일을 찾아 실행한다.
- `--version` → 인식된 Python 버전을 출력한다.

---

## 4. 예제

```powershell
python --version
```

실행 결과 예시:

```text
Python 3.13.15
```

버전 번호가 출력되면 터미널이 PATH를 통해 Python 실행 파일을 정상적으로 찾은 것이다.

---

## 5. 헷갈리는 개념 비교

|구분|Python 설치|PATH 등록|
|---|---|---|
|의미|Python 프로그램을 컴퓨터에 준비|터미널이 Python 실행 위치를 찾게 함|
|확인|설치 과정 완료|`python --version` 실행|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`PATH`|터미널이 실행 파일을 찾을 때 확인하는 경로 목록|
|`실행 경로`|프로그램의 실행 파일이 저장된 위치|

### 💻 주요 코드

|코드|의미|
|---|---|
|`python --version`|PATH를 통해 인식된 Python 버전 확인|

### ⭐ 한 줄 정리

> **PATH는 터미널이 Python과 같은 프로그램의 실행 파일을 찾도록 알려 주는 경로 목록이다.**

### 🔖 복습할 내용

- [ ] PATH의 역할 설명하기
- [ ] Python 설치 시 PATH 등록이 필요한 이유 설명하기
- [ ] Python 인식 여부를 버전 명령으로 확인하기
