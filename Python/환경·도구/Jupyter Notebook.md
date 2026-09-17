---
source:
  - "[[02 정리노트/week01/day02_08.07]]"
---

# Jupyter Notebook

## 1. 개념

Jupyter Notebook은 코드를 셀 단위로 작성하고 실행하는 환경이다. 파일은 `.ipynb` 확장자를 사용하며 VSCode에서는 Jupyter 확장 프로그램과 실행할 Python 커널이 필요하다.

> **핵심:** Jupyter Notebook은 선택한 Python 커널에서 셀 단위로 코드를 실행한다.

---

## 2. 쉽게 이해하기

코드를 여러 칸으로 나누어 필요한 셀을 실행하고 결과를 바로 확인하는 작업 문서라고 생각할 수 있다.

```text
Jupyter 확장 설치
  ↓
.ipynb 파일 생성
  ↓
Python 커널 선택
  ↓
Shift+Enter로 셀 실행
```

---

## 3. 사용 방법

- `.ipynb` → Jupyter Notebook 파일 확장자이다.
- `Jupyter` 확장 프로그램 → VSCode에서 노트북 작성과 실행을 지원한다.
- `Python 커널` → 노트북 코드를 실제로 실행하는 Python 환경이다.
- `Shift+Enter` → 현재 셀을 실행한다.

---

## 4. 예제

```python
name = "홍길동"
name
```

실행 결과:

```text
'홍길동'
```

선택한 Python 커널이 셀의 코드를 실행하고 변수에 저장된 값을 결과로 표시한다.

---

## 5. 헷갈리는 개념 비교

|구분|노트북 파일|Python 커널|
|---|---|---|
|역할|코드 셀과 결과 저장|셀의 Python 코드 실행|
|예시|`.ipynb`|프로젝트의 `.venv` 환경|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`Notebook`|코드를 셀 단위로 작성하고 실행하는 문서|
|`셀`|노트북에서 코드를 실행하는 단위|
|`커널`|노트북 코드를 실행하는 Python 환경|

### 💻 주요 코드

|코드|의미|
|---|---|
|`.ipynb`|Jupyter Notebook 파일 확장자|
|`Shift+Enter`|현재 셀 실행|

### ⭐ 한 줄 정리

> **Jupyter Notebook은 선택한 Python 커널을 사용해 코드를 셀 단위로 실행하고 결과를 확인하는 환경이다.**

### 🔖 복습할 내용

- [ ] 노트북 파일 확장자 기억하기
- [ ] Python 커널의 역할 설명하기
- [ ] 셀 실행 단축키 기억하기
