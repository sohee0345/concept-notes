# Open API와 인증키

## 1. 개념

Open API는 외부 프로그램이 정해진 방식으로 데이터를 요청하고 받을 수 있도록 공개된 기능이다.

공공데이터 API는 보통 인증키가 필요하며, 인증키는 `.env`에 저장해 코드와 분리한다.

> **핵심:** Open API는 인증키를 이용해 서버에 데이터를 요청하고 주로 JSON 형태로 응답을 받는다.

---

## 2. 쉽게 이해하기

API는 식당 주문 창구처럼 생각할 수 있다.

```text
요청 URL + 인증키
       ↓
     API 서버
       ↓
   JSON 데이터
```

---

## 3. 사용 방법

```python
import os
import requests
from dotenv import load_dotenv

load_dotenv()
api_key = os.getenv("API_KEY")

response = requests.get(url)
data = response.json()
```

---

## 4. 예제

```text
공공데이터 검색
→ API 활용 신청
→ 인증키 발급
→ .env 저장
→ requests로 요청
→ JSON 응답 사용
```

---

## 5. 헷갈리는 개념 비교

| 구분 | Open API | 웹크롤링 |
|---|---|---|
| 데이터 제공 | 정해진 형태로 제공 | HTML에서 직접 추출 |
| 주된 응답 | JSON 등 | HTML |
| 우선순위 | 제공되면 우선 사용 | API가 없을 때 활용 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- API Key → 사용 권한 확인
- JSON → API 응답에서 자주 쓰는 데이터 형식
- `.env` → 인증키 안전하게 관리

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `requests.get(url)` | API 요청 |
| `response.json()` | JSON 응답 변환 |
| `os.getenv('API_KEY')` | 인증키 불러오기 |

### ⭐ 한 줄 정리

> **Open API는 인증키를 이용해 서버에 데이터를 요청하고 주로 JSON 형태로 응답을 받는다.**

### 🔖 복습할 내용

- [ ] API 사용 전체 흐름
- [ ] 인증키를 코드에 직접 넣으면 안 되는 이유
- [ ] API와 크롤링 차이
