# Open API 요청

## 1. 개념

Open API는 외부 프로그램이 정해진 주소와 규칙으로 데이터를 요청할 수 있게 제공하는 기능이다. 공공데이터 API는 발급받은 인증키를 요청 URL에 포함하고 JSON 등의 응답을 받는다.

> **핵심:** 인증키와 요청 URL을 준비해 GET 요청을 보내고 JSON 응답을 Python 데이터로 변환한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
데이터와 인증키 신청
  ↓
요청 URL 구성
  ↓ requests.get()
서버 응답
  ↓ response.json()
Python 데이터
```

> **쉽게 말하면:** 정해진 주소에 인증키를 함께 보내 데이터를 요청하고 받은 답을 Python에서 쓸 수 있게 바꾸는 과정이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
import os
import requests
from dotenv import load_dotenv

load_dotenv()
api_key = os.getenv("FOOD_SAFETY_API_KEY")

url = f"http://openapi.foodsafetykorea.go.kr/api/{api_key}/I2570/json/1/5"
response = requests.get(url)
data = response.json()
```

- `api_key` → API 사용 권한을 확인하는 인증키
- `requests.get()` → URL에 GET 요청 전송
- `response` → 서버 응답 객체
- `response.json()` → JSON 응답을 Python 데이터로 변환

> **핵심:** 인증키는 코드에 직접 쓰지 않고 `.env`와 환경 변수로 불러온다.

------------------------------------------------------------------------

## 4. 예제

``` text
FOOD_SAFETY_API_KEY="발급받은인증키"
```

``` python
load_dotenv()
api_key = os.getenv("FOOD_SAFETY_API_KEY")

url = (
    "http://openapi.foodsafetykorea.go.kr/api/"
    f"{api_key}/I2570/json/1/5"
)

response = requests.get(url)
data = response.json()
```

### 코드 해석

- `I2570` → 실습에서 요청한 서비스 식별 부분
- `json` → 응답 형식
- `1/5` → 실습에서 요청한 데이터 범위

> **결과 해석:** 응답 JSON을 변환한 `data`를 딕셔너리와 리스트처럼 탐색할 수 있다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | Open API | 웹 크롤링 |
| --- | --- | --- |
| 데이터 | 제공자가 정한 응답 형식 | 웹페이지 HTML |
| 주요 변환 | `response.json()` | BeautifulSoup으로 분석 |
| 인증 | 인증키가 필요할 수 있음 | 페이지 방식에 따라 다름 |

------------------------------------------------------------------------

## 6. 주의할 점

- 인증키를 Python 코드에 직접 작성하지 않는다.
- `.env`의 환경 변수 이름과 `os.getenv()`의 이름을 같게 작성한다.
- API 문서의 서비스 이름, 응답 형식, 데이터 범위를 URL 순서에 맞춰 작성한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `Open API` | 외부 프로그램에 데이터를 제공하는 인터페이스 |
| `인증키` | API 사용 권한을 확인하는 값 |
| `JSON 응답` | API가 반환하는 구조화된 데이터 형식 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `requests.get(url)` | GET 요청 전송 |
| `response.json()` | JSON 응답 변환 |
| `os.getenv("API_KEY")` | 환경 변수의 인증키 읽기 |

### ⭐ 한 줄 정리

> **인증키를 포함한 URL로 Open API에 요청하고 JSON 응답을 Python 데이터로 변환한다.**

### 🔖 복습할 내용

- [ ] 공공데이터 API 신청부터 호출까지 순서 작성하기
- [ ] 인증키를 환경 변수로 불러오기
- [ ] JSON 응답을 Python 데이터로 변환하기
