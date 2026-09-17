---
source:
  - "[[02 정리노트/week02/day06_08.13]]"
---

# Streamlit

## 1. 개념

Streamlit은 Python 코드로 데이터와 상호작용하는 간단한 웹 애플리케이션을 만드는 외부 라이브러리이다. 출력 함수와 입력 위젯을 선언하여 웹 화면을 구성한다.

> **핵심:** Streamlit은 Python 함수로 텍스트, 데이터, 입력 위젯을 웹 화면에 배치한다.

---

## 2. 쉽게 이해하기

HTML을 직접 작성하기보다 Python 함수로 제목, 표, 버튼, 입력 칸을 순서대로 배치하는 방식이다.

```text
Python 코드 작성
  ↓ Streamlit 함수 실행
웹 화면과 위젯 생성
  ↓ 사용자 입력
앱 코드 다시 처리
```

---

## 3. 사용 방법

```python
import streamlit as st

st.title("제목")
name = st.text_input("이름을 입력하세요.")

if st.button("Say Hello"):
    st.write(f"Hello, {name}!")
```

- `st.title()` → 제목을 출력한다.
- `st.text_input()` → 문자열 입력 위젯을 만든다.
- `st.dataframe()` → DataFrame을 표시한다.
- `st.button()` → 클릭 여부에 따라 코드를 실행하는 버튼을 만든다.

---

## 4. 예제

```python
import streamlit as st

with st.form(key="my_form"):
    name = st.text_input("이름을 입력하세요.").strip()
    submitted = st.form_submit_button("Submit")

if submitted:
    st.write(f"Hello, {name}!")
```

Form 안의 여러 입력은 Submit 버튼을 눌렀을 때 한 번에 처리된다.

---

## 5. 헷갈리는 개념 비교

|구분|일반 위젯|Form|
|---|---|---|
|처리 시점|값이 바뀔 때 앱이 다시 실행될 수 있음|Submit 시점에 한 번에 처리|
|사용|개별 상호작용|여러 입력 묶기|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|Streamlit|Python으로 웹 앱을 만드는 외부 라이브러리|
|위젯|사용자의 입력이나 클릭을 받는 화면 요소|
|Form|여러 입력을 모아 제출 시 처리하는 영역|
|`pages` 폴더|여러 페이지 파일을 배치하는 폴더|

### 💻 주요 코드

|코드|의미|
|---|---|
|`st.dataframe(df)`|DataFrame 표시|
|`st.button()`|버튼 생성|
|`st.form()`|입력 Form 생성|
|`st.form_submit_button()`|Form 제출 버튼 생성|

### ⭐ 한 줄 정리

> **Streamlit은 Python 출력 함수와 입력 위젯을 선언하여 상호작용하는 웹 앱을 구성한다.**

### 🔖 복습할 내용

- [ ] 표준 라이브러리와 Streamlit 구분하기
- [ ] 주요 출력 함수와 위젯 사용하기
- [ ] 일반 위젯과 Form의 처리 시점 비교하기
