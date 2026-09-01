# HTTP 요청과 requests

## 1. 개념

`requests`는 Python에서 웹 서버에 HTTP 요청을 보내고 응답을 받을 때 사용하는 라이브러리다.

응답 객체에서는 `status_code`, `text`, `json()` 등을 통해 서버의 응답을 확인할 수 있다.

> **핵심:** requests를 사용하면 Python에서 웹 서버에 요청을 보내고 응답 데이터를 받을 수 있다.

---

## 2. 쉽게 이해하기

웹 브라우저 대신 Python이 서버에 자료를 요청한다고 생각하면 된다.

```text
Python
  ↓ 요청
Web Server
  ↓ 응답
response
```

---

## 3. 사용 방법

```python
import requests

response = requests.get(
    url="https://example.com",
    params={"userId": "1"},
    headers={"User-Agent": "Mozilla/5.0"}
)

print(response.status_code)
```

---

## 4. 예제

```python
response.json()   # JSON 응답
response.text     # HTML 등 문자열 응답
```

상태 코드는 대략 다음처럼 구분한다.

```text
200번대 → 성공
300번대 → 이동
400번대 → 요청 오류
500번대 → 서버 오류
```

---

## 5. 헷갈리는 개념 비교

| 구분 | 의미 |
|---|---|
| `params` | Query Parameter |
| `headers` | 요청과 함께 보내는 추가 정보 |
| `User-Agent` | 브라우저·환경 정보 |
| `Referer` | 직전에 방문한 URL 정보 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- `response` → 서버 응답
- `status_code` → 요청 결과
- `params` → URL에 전달할 조건
- `headers` → 추가 요청 정보

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `requests.get()` | GET 요청 |
| `response.status_code` | 상태 코드 확인 |
| `response.json()` | JSON 변환 |
| `response.text` | 문자열 응답 확인 |

### ⭐ 한 줄 정리

> **requests를 사용하면 Python에서 웹 서버에 요청을 보내고 응답 데이터를 받을 수 있다.**

### 🔖 복습할 내용

- [ ] 200/400/500번대 의미
- [ ] `params`와 `headers` 차이
- [ ] `json()`과 `text` 차이
