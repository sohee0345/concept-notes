# Streamlit

## 1. 개념

Streamlit은 Python 코드로 텍스트, 입력 위젯, 표 등을 배치하여 웹 애플리케이션을 만드는 외부 라이브러리이다.

> **핵심:** Streamlit에서는 `st`로 시작하는 함수를 호출해 웹 화면과 사용자 입력 동작을 구성한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
Python 코드 작성
  ↓
Streamlit 함수로 화면 요소 배치
  ↓
사용자가 텍스트 입력·버튼 클릭
  ↓
조건에 맞는 결과 표시
```

> **쉽게 말하면:** HTML을 직접 작성하지 않고 Python 함수로 웹 화면을 조립하는 도구이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
import streamlit as st

st.title("제목")
st.header("머리글")
st.caption("설명")
st.text("일반 텍스트")
st.markdown("**마크다운**")
st.code("print('Hello')", language="python")

name = st.text_input("이름을 입력하세요.")
```

- `st.title()` → 제목 표시
- `st.header()` → 머리글 표시
- `st.caption()` → 짧은 설명 표시
- `st.text()` → 일반 텍스트 표시
- `st.markdown()` → Markdown 형식 표시
- `st.code()` → 코드 블록 표시
- `st.text_input()` → 사용자에게 문자열 입력받기

> **핵심:** 출력 함수는 화면에 내용을 표시하고 입력 위젯은 사용자의 값을 변수에 반환한다.

### 재실행과 `session_state`

Streamlit은 사용자가 입력하거나 위젯을 조작하면 코드가 위에서부터 다시 실행될 수 있다. 다시 실행되어도 유지해야 하는 값은 `st.session_state`에 저장한다.

``` python
if "history" not in st.session_state:
    st.session_state.history = []
```

- `"history" not in st.session_state` → 처음 실행되어 아직 이력이 없는지 확인
- `st.session_state.history` → 현재 세션에서 유지할 대화 이력

------------------------------------------------------------------------

## 4. 예제

### DataFrame 표시

``` python
import streamlit as st
import pandas as pd
import numpy as np

df = pd.DataFrame(
    np.random.randn(5, 5),
    columns=[f"col_{i}" for i in range(5)],
)

st.title("DataFrame :innocent:")
st.dataframe(df.style.highlight_max(axis=0))
```

`column_config`를 사용하면 컬럼별 표시 형식을 설정할 수 있다.

``` python
st.dataframe(
    df,
    column_config={
        "url": st.column_config.LinkColumn("App URL"),
        "stars": st.column_config.NumberColumn(
            "GitHub Stars", format="%d 🌟"
        ),
        "views_history": st.column_config.LineChartColumn(
            "Views history", y_min=0, y_max=5000
        ),
    },
)
```

### 버튼과 Form

``` python
if st.button("Say Hello"):
    st.write("Hello World!")

with st.form(key="my_form"):
    text_input = st.text_input("Enter your name").strip()
    submitted = st.form_submit_button("Submit")

if submitted:
    st.write(f"Hello, {text_input}!")

st.link_button("go to naver", "https://www.naver.com")
```

### 채팅 UI와 대화 이력

``` python
import enum
import streamlit as st

class ROLE(enum.Enum):
    user = enum.auto()
    assistant = enum.auto()

def show_msg(role: ROLE, msg: str, is_history=False) -> None:
    with st.chat_message(role.name):
        st.markdown(msg)

    if not is_history:
        st.session_state.history.append({
            "role": role,
            "msg": msg,
        })

if "history" not in st.session_state:
    st.session_state.history = []

for history in st.session_state.history:
    show_msg(**history, is_history=True)

user_input = st.chat_input("메시지 입력해주세요.")
```

- `st.chat_input()` → 채팅 메시지 입력창
- `st.chat_message(role)` → 사용자 또는 AI 역할의 메시지 영역
- `history` → 역할과 메시지를 순서대로 저장한 리스트
- `is_history=True` → 과거 메시지를 복원하면서 같은 내용을 다시 저장하지 않도록 구분

### 외부 자원 캐싱

``` python
from groq import Groq

@st.cache_resource
def get_client():
    return Groq()
```

`st.cache_resource`는 API 클라이언트처럼 다시 실행할 때마다 새로 만들 필요가 없는 자원을 재사용할 때 사용한다.

### 코드 해석

- `st.dataframe()` → DataFrame을 웹 화면에 표시한다.
- `highlight_max(axis=0)` → 각 열의 최댓값을 강조한다.
- `st.button()` → 클릭하면 `True`를 반환하는 버튼을 만든다.
- `st.form()` → 여러 입력 위젯을 하나의 Form으로 묶는다.
- `st.form_submit_button()` → Form 입력을 제출하는 버튼을 만든다.
- `st.link_button()` → 지정한 URL로 이동하는 버튼을 만든다.
- `st.chat_input()` → 채팅 입력창을 만든다.
- `st.chat_message()` → 역할에 맞는 채팅 메시지 영역을 만든다.
- `st.session_state` → 재실행 사이에 유지할 상태를 저장한다.
- `st.cache_resource` → 클라이언트 같은 자원을 캐싱한다.

> **결과 해석:** 버튼의 반환값과 Form 제출 여부를 조건문으로 확인해 사용자 동작에 맞는 내용을 화면에 표시한다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | 일반 위젯 | Form 내부 위젯 | `session_state` |
| --- | --- | --- | --- |
| 역할 | 개별 입력·동작 | 여러 입력을 묶음 | 재실행 사이에 값 유지 |
| 처리 시점 | 위젯 상태가 변경될 때 | Submit 버튼을 누를 때 | 앱이 다시 실행된 뒤에도 조회 |
| 예시 | `st.button()` | `st.form_submit_button()` | `st.session_state.history` |

------------------------------------------------------------------------

## 6. 주의할 점

- Streamlit은 Python 표준 라이브러리가 아니므로 별도 설치가 필요하다.
- Form에서 만든 Submit 변수는 `with st.form(...)` 블록 밖에서 조건문으로 확인할 수 있다.
- `.strip()`을 사용하면 입력 문자열 양 끝의 불필요한 공백을 제거할 수 있다.
- DataFrame의 `column_config` 키는 표시할 DataFrame의 컬럼 이름과 맞아야 한다.
- `session_state` 값은 키가 없을 때만 초기화해야 기존 이력이 사라지지 않는다.
- 과거 이력을 화면에 다시 표시할 때 같은 메시지를 `history`에 중복 저장하지 않는다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `Streamlit` | Python으로 웹 앱을 만드는 외부 라이브러리 |
| `위젯` | 텍스트 입력이나 버튼처럼 사용자와 상호작용하는 요소 |
| `DataFrame 표시` | 표 데이터를 웹 화면에 출력하는 기능 |
| `Form` | 여러 입력을 Submit 시점에 함께 처리하는 영역 |
| `다중 페이지` | `pages` 폴더의 Python 파일로 화면을 분리하는 구조 |
| `session_state` | 앱 재실행 사이에 유지할 상태 저장 |
| `채팅 이력` | 사용자와 AI의 역할·메시지를 순서대로 저장한 데이터 |
| `resource cache` | 클라이언트 같은 자원을 재사용하는 캐시 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `import streamlit as st` | Streamlit 불러오기 |
| `st.text_input()` | 문자열 입력 위젯 생성 |
| `st.dataframe()` | DataFrame 표시 |
| `st.column_config` | 컬럼 표시 형식 설정 |
| `st.button()` | 일반 버튼 생성 |
| `st.form()` | 여러 입력을 Form으로 묶기 |
| `st.form_submit_button()` | Form 제출 버튼 생성 |
| `st.chat_input()` | 채팅 메시지 입력창 생성 |
| `st.chat_message()` | 역할별 채팅 메시지 표시 |
| `st.session_state` | 세션 상태 저장 |
| `@st.cache_resource` | 외부 자원 캐싱 |

### ⭐ 한 줄 정리

> **Streamlit은 Python 함수로 웹 화면을 구성하고 `session_state`로 재실행 사이의 상태와 대화 이력을 유지한다.**

### 🔖 복습할 내용

- [ ] 텍스트 출력 함수별 역할 구분하기
- [ ] DataFrame 컬럼 표시 형식 설정하기
- [ ] 일반 버튼과 Form 제출 버튼 비교하기
- [ ] `pages` 폴더로 페이지 분리하기
- [ ] `session_state`에 대화 이력 초기화하기
- [ ] `chat_input`과 `chat_message`로 채팅 UI 구성하기
- [ ] 과거 이력을 복원할 때 중복 저장 방지하기
