---
source:
  - "[[02 정리노트/week03/day11_08.21]]"
---

# Open API 요청

## 1. 개념

Open API는 정해진 주소와 형식으로 요청하면 외부 서비스가 데이터를 반환하는 인터페이스이다. 공공데이터 API는 활용 신청과 인증키 발급 후 요청한다.

> **핵심:** 인증키를 안전하게 관리하고 요청의 상태 코드와 실제 응답 구조를 함께 확인한다.

---

## 2. 쉽게 이해하기

서비스가 공개한 주문서 형식에 맞춰 주소와 인증키를 보내면 약속된 데이터가 돌아오는 구조이다.

```text
활용 신청 → 인증키 발급 → 요청 전송 → 상태 코드·응답 확인
```

---

## 3. 사용 방법

```python
response = requests.get(url)
print(response.status_code)
data = response.json()
```

- `requests.get()` → HTTP GET 요청을 보낸다.
- `status_code` → 요청 처리 결과를 나타낸다.
- `response.json()` → JSON 본문을 Python 딕셔너리나 리스트로 변환한다.

---

## 4. 예제

```python
api_key = os.getenv("FOOD_SAFETY_API_KEY")
url = f"http://openapi.foodsafetykorea.go.kr/api/{api_key}/I2570/json/1/5"
response = requests.get(url)
print(response.status_code)
data = response.json()
```

상태 코드 `200`은 정상 처리를 뜻하며 응답 구조를 확인해 원하는 데이터 위치를 찾는다.

---

## 5. 헷갈리는 개념 비교

|구분|상태 코드|응답 본문|
|---|---|---|
|의미|요청 처리 상태|반환된 실제 데이터|
|확인|`status_code`|`json()`|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|Open API|외부 데이터를 정해진 형식으로 제공하는 인터페이스|
|인증키|API 사용 권한을 확인하는 값|
|JSON 응답|구조화된 응답 데이터|

### 💻 주요 코드

|코드|의미|
|---|---|
|`requests.get(url)`|GET 요청 전송|
|`response.status_code`|상태 코드 확인|
|`response.json()`|JSON 응답 변환|

### ⭐ 한 줄 정리

> **Open API는 인증키와 요청 형식에 맞춰 호출하고 상태 코드와 응답 데이터를 검증한다.**

### 🔖 복습할 내용

- [ ] API 활용 절차 설명하기
- [ ] 인증키를 환경 변수로 관리하기
- [ ] 상태 코드와 JSON 응답 확인하기
