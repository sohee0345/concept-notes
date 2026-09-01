# Streamlit chatbot

## 1. 개념
Streamlit에서 채팅 UI를 만들고, 앱이 다시 실행되어도 대화 기록을 유지하려면 `st.session_state`를 사용한다.

> **핵심:** 입력은 `st.chat_input()`, 출력은 `st.chat_message()`, 대화 기록은 `st.session_state`에 저장한다.

---

## 2. 쉽게 이해하기
```text
사용자 입력
  ↓
st.chat_input()
  ↓
session_state에 저장
  ↓
답변 생성
  ↓
st.chat_message()로 출력
```

---

## 3. 사용 방법
```python
import streamlit as st

if "messages" not in st.session_state:
    st.session_state.messages = []

user_input = st.chat_input("메시지를 입력하세요")
```

- `st.chat_input()` → 채팅 입력창
- `st.chat_message()` → 역할별 채팅 메시지 표시
- `st.session_state` → 앱 재실행 후에도 유지해야 하는 값 저장

---

## 4. 예제
```python
if user_input:
    st.session_state.messages.append(
        {"role": "user", "content": user_input}
    )

for message in st.session_state.messages:
    st.chat_message(message["role"]).write(message["content"])
```

실행 흐름:
```text
입력 → 저장 → 응답 생성 → 저장 → 전체 대화 출력
```

---

## 5. 헷갈리는 개념 비교
|구분|일반 변수|`st.session_state`|
|---|---|---|
|재실행 후 값|초기화될 수 있음|세션 동안 유지 가능|
|사용|일시적 계산|대화 기록 등 상태 저장|

---

## 🟦 핵심 정리

### 💡 주요 개념
chat_input, chat_message, session_state, 대화 기록

### 💻 주요 코드
|코드|의미|
|---|---|
|`st.chat_input()`|채팅 입력|
|`st.chat_message()`|채팅 출력|
|`st.session_state`|상태 저장|

### ⭐ 한 줄 정리
> **Streamlit 챗봇은 입력·출력 컴포넌트와 session_state를 함께 사용해 대화 상태를 유지한다.**

### 🔖 복습할 내용
- [ ] session_state가 필요한 이유
- [ ] 메시지 저장 구조
- [ ] 챗봇 동작 순서
