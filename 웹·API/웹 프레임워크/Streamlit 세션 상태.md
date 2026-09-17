---
source:
  - "[[02 정리노트/week02/day07_08.14]]"
---

# Streamlit 세션 상태

## 1. 개념

Streamlit은 위젯을 조작하면 스크립트를 위에서부터 다시 실행할 수 있다. `st.session_state`는 이 재실행 사이에도 대화 이력처럼 유지해야 하는 값을 저장한다.

> **핵심:** 일반 변수는 재실행 때 다시 만들어지므로 지속할 데이터는 세션 상태에 저장한다.

---

## 2. 쉽게 이해하기

스크립트가 다시 시작될 때마다 일반 메모장은 지워지지만 세션 상태라는 보관함의 내용은 유지되는 것과 같다.

```text
위젯 조작
  ↓ 스크립트 재실행
session_state에서 기존 값 복원
  ↓
새 값을 추가해 다음 실행까지 유지
```

---

## 3. 사용 방법

```python
if "history" not in st.session_state:
    st.session_state.history = []

st.session_state.history.append({
    "role": ROLE.user,
    "msg": user_input
})
```

- 키가 없을 때만 초기화하여 기존 값을 지우지 않는다.
- 저장된 이력을 순서대로 출력하여 화면을 복원한다.
- 새 메시지는 사용자와 챗봇 답변을 각각 한 번씩 저장한다.

---

## 4. 예제

```python
if "history" not in st.session_state:
    st.session_state.history = []

for history in st.session_state.history:
    show_msg(**history, is_history=True)
```

저장된 메시지는 화면에만 다시 표시한다. 복원 중 같은 메시지를 이력에 추가하면 중복 저장될 수 있다.

---

## 5. 헷갈리는 개념 비교

|구분|일반 변수|`st.session_state`|
|---|---|---|
|재실행 후|다시 생성|값 유지|
|사용|현재 실행의 임시 값|대화 이력 등 지속할 값|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|재실행|위젯 조작 후 스크립트를 처음부터 다시 실행하는 동작|
|세션 상태|재실행 사이에 유지할 데이터를 저장하는 공간|
|이력 복원|저장된 메시지를 다시 화면에 표시하는 과정|

### 💻 주요 코드

|코드|의미|
|---|---|
|`st.session_state`|세션 상태 접근|
|`if "history" not in st.session_state`|최초 한 번만 이력 초기화|
|`st.session_state.history.append(...)`|새 메시지 저장|

### ⭐ 한 줄 정리

> **Streamlit 세션 상태는 스크립트 재실행 사이에도 대화 이력 같은 값을 유지한다.**

### 🔖 복습할 내용

- [ ] Streamlit 재실행 방식 설명하기
- [ ] 이력을 최초 한 번만 초기화하기
- [ ] 복원과 새 메시지 저장 구분하기
