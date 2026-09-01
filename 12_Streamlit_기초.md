# Streamlit 기초

## 1. 개념
Streamlit은 파이썬 코드만으로 간단한 웹 화면을 만들 수 있게 해주는 라이브러리다.

> **핵심:** `st.`으로 시작하는 함수를 사용해 텍스트, 데이터, 입력창, 버튼 등을 화면에 배치한다.

---

## 2. 쉽게 이해하기
```text
Python 코드
  ↓
Streamlit 컴포넌트
  ↓
웹 화면
```

---

## 3. 사용 방법
```python
import streamlit as st

st.title("제목")
name = st.text_input("이름")

if st.button("확인"):
    st.write(name)
```

- `st.title()` → 큰 제목
- `st.markdown()` → Markdown 출력
- `st.write()` → 값 출력
- `st.dataframe()` → DataFrame 출력
- `st.text_input()` → 텍스트 입력
- `st.button()` → 버튼 생성
- `st.form()` → 여러 입력을 묶어 제출

---

## 4. 예제
```python
import streamlit as st

with st.form("my_form"):
    name = st.text_input("이름")
    submitted = st.form_submit_button("제출")

if submitted:
    st.write(name)
```

실행 결과:
```text
사용자가 이름을 입력하고 제출 버튼을 누르면 입력값이 화면에 출력된다.
```

---

## 5. 헷갈리는 개념 비교
|구분|일반 widget|`st.form()`|
|---|---|---|
|실행|값 변경 시 앱이 다시 실행될 수 있음|Submit 시 입력을 한 번에 처리|

---

## 🟦 핵심 정리

### 💡 주요 개념
Streamlit, widget, form

### 💻 주요 코드
|코드|의미|
|---|---|
|`st.title()`|제목 출력|
|`st.text_input()`|문자 입력|
|`st.button()`|버튼 생성|

### ⭐ 한 줄 정리
> **Streamlit은 파이썬 함수로 입력과 출력을 배치해 빠르게 웹 앱을 만들 수 있게 해준다.**

### 🔖 복습할 내용
- [ ] 자주 쓰는 `st.` 함수
- [ ] button 동작
- [ ] form 사용 이유
