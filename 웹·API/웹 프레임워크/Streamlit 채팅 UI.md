---
source:
  - "[[02 정리노트/week02/day07_08.14]]"
---

# Streamlit 채팅 UI

## 1. 개념

Streamlit 채팅 UI는 `st.chat_input()`으로 메시지를 받고 `st.chat_message()`로 사용자와 챗봇의 역할에 맞는 메시지 영역을 만든다. 입력, 응답 생성, 저장, 출력 순서로 처리한다.

> **핵심:** 현재 입력과 이전 이력을 구분하여 답변을 만들고 사용자와 챗봇 메시지를 각각 한 번 저장·출력한다.

---

## 2. 쉽게 이해하기

입력창에서 받은 새 메시지를 이전 대화와 함께 응답 로직에 전달하고, 완성된 두 메시지를 역할별 말풍선에 표시하는 흐름이다.

```text
이전 이력 복원
  ↓ 새 메시지 입력
응답 생성
  ↓
사용자·챗봇 메시지 저장
  ↓
역할별 화면 출력
```

---

## 3. 사용 방법

```python
user_input = st.chat_input("메시지를 입력하세요.")

if user_input:
    with st.chat_message("user"):
        st.markdown(user_input)
```

- `st.chat_input()` → 메시지 입력 위젯을 만든다.
- `st.chat_message("user")` → 사용자 메시지 영역을 만든다.
- `st.chat_message("assistant")` → 챗봇 메시지 영역을 만든다.
- `@st.cache_resource` → API 클라이언트처럼 생성 비용이 있는 자원을 재사용한다.

---

## 4. 예제

```python
if user_input:
    previous_messages = [
        {"role": item["role"].name, "content": item["msg"]}
        for item in st.session_state.history
    ]
    request_messages = previous_messages + [
        {"role": "user", "content": user_input}
    ]

    answer = request_ai(request_messages)
    show_msg(ROLE.user, user_input)
    show_msg(ROLE.assistant, answer)
```

이전 이력과 현재 입력을 구분해 요청을 만들고, 완성된 사용자 메시지와 답변을 각각 한 번 처리한다.

---

## 5. 헷갈리는 개념 비교

|구분|`chat_input`|`chat_message`|
|---|---|---|
|역할|사용자 메시지 입력|역할별 메시지 출력 영역|
|결과|제출된 문자열|`with` 블록의 화면 영역|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|채팅 입력|사용자가 새 메시지를 제출하는 과정|
|역할별 메시지|사용자와 챗봇을 구분해 출력하는 영역|
|자원 캐시|생성 비용이 있는 자원을 만들어 재사용하는 기능|

### 💻 주요 코드

|코드|의미|
|---|---|
|`st.chat_input()`|채팅 입력창 생성|
|`st.chat_message(role)`|역할별 메시지 영역 생성|
|`@st.cache_resource`|생성한 자원 캐시|

### ⭐ 한 줄 정리

> **Streamlit 채팅 UI는 이전 이력과 현재 입력을 구분하여 응답을 만들고 역할별 메시지로 출력한다.**

### 🔖 복습할 내용

- [ ] 채팅 입력부터 출력까지의 순서 설명하기
- [ ] 이전 이력과 현재 입력 구분하기
- [ ] 사용자와 챗봇 메시지를 한 번씩 저장하기
