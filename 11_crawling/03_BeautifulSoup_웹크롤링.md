# BeautifulSoup 웹크롤링

## 1. 개념

웹크롤링은 웹페이지의 HTML에서 필요한 정보를 직접 추출하는 작업이다.

`requests`로 HTML을 가져오고 `BeautifulSoup`으로 구조를 분석한 뒤 `select()`, `find_all()`, `get_text()` 등으로 원하는 데이터를 찾는다.

> **핵심:** 웹크롤링의 기본은 requests로 HTML을 받고 BeautifulSoup으로 필요한 요소와 텍스트를 추출하는 것이다.

---

## 2. 쉽게 이해하기

```text
웹페이지 요청
   ↓
response.text
   ↓
BeautifulSoup
   ↓
HTML 요소 찾기
   ↓
텍스트 추출
```

---

## 3. 사용 방법

```python
import requests
from bs4 import BeautifulSoup

response = requests.get("https://example.com")
soup = BeautifulSoup(response.text, "html.parser")

items = soup.select(".item")
```

---

## 4. 예제

```python
soup.select("#newsct")
element.find_all("div", class_="o-price")
element.get_text()
```

반복해서 여러 페이지를 요청할 때는 서버 부담을 줄이기 위해 요청 사이에 간격을 둘 수 있다.

```python
import time
time.sleep(1)
```

---

## 5. 헷갈리는 개념 비교

| 메서드 | 역할 |
|---|---|
| `select()` | CSS 선택자로 요소 찾기 |
| `find_all()` | 조건에 맞는 요소 모두 찾기 |
| `get_text()` | 태그를 제외한 텍스트 추출 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- HTML → 웹페이지 구조
- BeautifulSoup → HTML 분석
- CSS 선택자 → 원하는 요소 지정
- `time.sleep()` → 반복 요청 사이 대기

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `BeautifulSoup(response.text, 'html.parser')` | HTML 분석 객체 생성 |
| `soup.select()` | CSS 선택자로 검색 |
| `find_all()` | 조건 요소 모두 검색 |
| `get_text()` | 텍스트만 추출 |
| `time.sleep(1)` | 1초 대기 |

### ⭐ 한 줄 정리

> **웹크롤링의 기본은 requests로 HTML을 받고 BeautifulSoup으로 필요한 요소와 텍스트를 추출하는 것이다.**

### 🔖 복습할 내용

- [ ] `select()`와 `find_all()` 차이
- [ ] id와 class CSS 선택자
- [ ] 반복 요청 시 대기 시간을 두는 이유
