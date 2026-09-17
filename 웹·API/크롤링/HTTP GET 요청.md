---
source:
  - "[[02 정리노트/week04/day12_08.24]]"
---

# HTTP GET 요청

## 1. 개념

HTTP GET 요청은 URL의 자원을 조회하는 요청이다. 쿼리 파라미터는 조회 조건을, Header는 요청 환경과 같은 부가 정보를 전달한다.

> **핵심:** URL, params, headers를 구분하고 상태 코드와 응답 형식에 맞게 결과를 읽는다.

---

## 2. 쉽게 이해하기

URL이 목적지라면 params는 주문 조건이고 headers는 요청을 보낸 환경을 설명하는 부가 정보이다.

```text
URL + Query Parameter + Header → GET 요청 → Response
```

---

## 3. 사용 방법

```python
response = requests.get(
    url="https://example.com/posts",
    params={"userId": "1"},
    headers={"User-Agent": "Mozilla/5.0"},
)
```

- `params` → URL의 `?` 뒤에 붙는 조회 조건이다.
- `User-Agent` → 요청을 보내는 실행 환경을 나타낸다.
- `Referer` → 이전에 방문한 페이지 주소를 나타낸다.
- `status_code` → 서버 처리 결과를 숫자로 나타낸다.

---

## 4. 예제

```python
if 200 <= response.status_code < 300:
    data = response.json()
```

200번대 상태 코드는 요청이 정상 처리되었음을 나타내며 JSON 응답은 Python 자료구조로 변환한다.

---

## 5. 헷갈리는 개념 비교

|구분|params|headers|
|---|---|---|
|역할|조회 조건 전달|요청 부가 정보 전달|
|예시|`userId=1`|`User-Agent`, `Referer`|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|GET|자원을 조회하는 HTTP 요청 방식|
|Query Parameter|URL과 함께 전달하는 조회 조건|
|Header|요청·응답의 부가 정보|
|상태 코드|서버 처리 결과|

### 💻 주요 코드

|코드|의미|
|---|---|
|`requests.get()`|GET 요청 전송|
|`response.status_code`|상태 코드 확인|
|`response.json()`|JSON 응답 변환|

### ⭐ 한 줄 정리

> **HTTP GET 요청은 URL에 조회 조건과 헤더를 더해 자원을 요청하고 응답 상태와 형식을 확인한다.**

### 🔖 복습할 내용

- [ ] params와 headers 구분하기
- [ ] 상태 코드 범위 설명하기
- [ ] JSON과 HTML 응답 처리 구분하기
