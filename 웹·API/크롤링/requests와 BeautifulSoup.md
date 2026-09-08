# requests와 BeautifulSoup

## 1. 개념

`requests`는 웹 서버에 HTTP 요청을 보내 응답을 받는 라이브러리이고, BeautifulSoup은 받은 HTML이나 XML 문서의 구조를 분석하는 라이브러리이다.

> **핵심:** requests가 문서를 가져오고 BeautifulSoup이 문서 안에서 정보를 찾을 수 있게 구조를 분석한다.

------------------------------------------------------------------------

## 2. 처리 흐름

```text
URL
  ↓ requests.get()
HTTP 응답
  ↓ response.text
HTML 문자열
  ↓ BeautifulSoup
탐색 가능한 문서 객체
```

------------------------------------------------------------------------

## 3. 예제

```python
import requests
from bs4 import BeautifulSoup

response = requests.get("https://example.com")
soup = BeautifulSoup(response.text, "html.parser")
```

- `requests.get()` → URL로 GET 요청을 보낸다.
- `response.text` → 응답 본문을 문자열로 읽는다.
- `html.parser` → HTML 구조를 분석할 파서를 지정한다.
- `soup` → 태그와 텍스트를 찾을 수 있는 객체이다.

------------------------------------------------------------------------

## 4. JSON 응답과의 차이

BeautifulSoup은 HTML이나 XML 같은 마크업 문서를 분석한다. API가 JSON을 반환할 때는 BeautifulSoup이 아니라 `response.json()`을 사용해 딕셔너리나 리스트로 변환한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| requests | 웹 서버에 요청을 보내 응답을 받는다. |
| BeautifulSoup | HTML·XML 문서 구조를 분석한다. |
| 파서 | 문자열 문서를 구조화하여 해석한다. |

### ⭐ 한 줄 정리

> **requests로 HTML을 받고 BeautifulSoup으로 구조를 분석해 필요한 태그와 텍스트를 찾는다.**

### 🔖 복습할 내용

- [ ] 요청과 HTML 분석 단계 구분하기
- [ ] `response.text`의 역할 설명하기
- [ ] HTML 응답과 JSON 응답 처리 방식 구분하기

