# LLM Chat API 호출

## 1. 개념

LLM Chat API 호출은 사용자와 AI의 대화 이력을 역할과 내용으로 구성해 모델에 보내고 응답 메시지를 받는 과정이다. 실습에서는 Groq 클라이언트의 Chat Completions 방식으로 호출했다.

> **핵심:** 대화 순서를 유지한 메시지 목록과 모델 이름을 API에 전달하고 응답 객체에서 생성된 내용을 꺼낸다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
내부 대화 이력
  ↓ role·content 형식으로 변환
API 클라이언트에 messages와 model 전달
  ↓
응답 객체 수신
  ↓
assistant 메시지 내용 추출
```

> **쉽게 말하면:** 지금까지의 대화를 API가 이해하는 형식으로 정리해 보내고 답변 부분만 꺼내는 과정이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
import streamlit as st
from groq import Groq
from dotenv import load_dotenv

@st.cache_resource
def get_client():
    load_dotenv()
    return Groq()
```

- `load_dotenv()` → `.env` 값을 환경 변수로 불러오기
- `Groq()` → API 클라이언트 생성
- `@st.cache_resource` → 생성한 클라이언트를 다시 실행해도 재사용

> **핵심:** 클라이언트는 한 번 만든 뒤 캐싱하여 Streamlit 재실행마다 새로 만들지 않는다.

------------------------------------------------------------------------

## 4. 예제

``` python
messages = [
    {
        "role": history["role"].name,
        "content": history["msg"],
    }
    for history in st.session_state.history
]

client = get_client()
response = client.chat.completions.create(
    messages=messages,
    model="openai/gpt-oss-120b",
)

answer = response.choices[0].message.content
```

### 코드 해석

- `messages` → 대화 순서대로 정리한 역할과 메시지 목록
- `role` → `user`, `assistant` 같은 메시지 작성자 역할
- `content` → 실제 메시지 내용
- `model` → 응답을 생성할 모델 이름
- `response.choices[0].message.content` → 첫 번째 응답의 메시지 내용

> **결과 해석:** API가 반환한 응답 객체에서 AI가 생성한 문자열을 가져와 채팅 화면에 표시할 수 있다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | Streamlit 내부 이력 | API 메시지 |
| --- | --- | --- |
| 역할 키 | `role` | `role` |
| 내용 키 | `msg` | `content` |
| 역할 값 | `ROLE` Enum | `user`, `assistant` 문자열 |
| 목적 | 화면 상태 저장 | 모델에 대화 전달 |

------------------------------------------------------------------------

## 6. 주의할 점

- 사용자 메시지를 이력에 저장한 뒤 같은 입력을 API 목록에 다시 추가하면 최신 메시지가 중복될 수 있다.
- 대화 순서가 바뀌지 않도록 저장된 이력을 차례대로 변환한다.
- 응답 내용은 응답 객체의 `choices[0].message.content`에서 가져온다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `API 클라이언트` | 외부 API와 통신하는 객체 |
| `messages` | 역할과 내용으로 구성된 대화 목록 |
| `model` | 응답 생성에 사용할 모델 이름 |
| `응답 객체` | 모델의 생성 결과가 담긴 API 반환값 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `load_dotenv()` | 환경 변수 불러오기 |
| `@st.cache_resource` | 클라이언트 자원 캐싱 |
| `client.chat.completions.create()` | Chat API 호출 |
| `response.choices[0].message.content` | AI 응답 내용 추출 |

### ⭐ 한 줄 정리

> **대화 이력을 `role`과 `content` 형식으로 변환해 모델에 전달하고 응답 객체에서 AI 메시지를 추출한다.**

### 🔖 복습할 내용

- [ ] 내부 이력을 API 메시지 형식으로 변환하기
- [ ] `cache_resource`를 사용하는 이유 설명하기
- [ ] 최신 사용자 메시지 중복 여부 확인하기
