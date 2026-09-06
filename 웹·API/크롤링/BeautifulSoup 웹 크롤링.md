# BeautifulSoup 웹 크롤링

## 1. 개념

웹 크롤링은 웹페이지를 요청하고 HTML에서 필요한 정보를 추출하는 방법이다. `requests`로 HTML을 받고 BeautifulSoup으로 분석 가능한 객체를 만든다.

> **핵심:** 웹페이지의 HTML을 요청한 뒤 파싱하여 필요한 정보를 찾는다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
웹페이지 URL
  ↓ requests.get()
HTML 문자열
  ↓ BeautifulSoup
분석 가능한 HTML 객체
  ↓
필요한 정보 추출
```

> **쉽게 말하면:** 웹페이지의 원본 문서를 가져와 구조를 읽을 수 있게 정리한 뒤 필요한 부분을 찾는 것이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
import requests
from bs4 import BeautifulSoup

response = requests.get("https://example.com")
soup = BeautifulSoup(response.text, "html.parser")
```

- `requests.get()` → 웹페이지 요청
- `response.text` → 서버에서 받은 HTML 문자열
- `BeautifulSoup()` → HTML 분석 객체 생성
- `html.parser` → HTML 파싱 방식

> **핵심:** API의 JSON과 달리 웹페이지 응답은 HTML 구조를 분석해 필요한 요소를 찾아야 한다.

### 요소 검색과 텍스트 추출

``` python
areas = soup.select("body > div")
prices = areas[0].find_all("div", class_="o-price")
price_text = prices[0].get_text().strip()
```

- `select()` → CSS 선택자에 맞는 모든 요소를 리스트로 반환
- `find()` → 태그와 속성 조건에 맞는 첫 요소 반환
- `find_all()` → 조건에 맞는 모든 요소를 리스트로 반환
- `get_text()` → HTML 태그를 제외한 내부 텍스트 반환
- `strip()` → 텍스트 양 끝의 공백 제거

CSS 선택자 예시:

``` python
soup.select("#newsct")    # id가 newsct인 요소
soup.select("body > div") # body 바로 아래의 div
```

------------------------------------------------------------------------

## 4. 예제

``` python
import time
import requests
from bs4 import BeautifulSoup

for page in range(1, 6):
    response = requests.get(
        f"https://example.com/list?page={page}"
    )
    soup = BeautifulSoup(response.text, "html.parser")

    # 필요한 정보 추출

    time.sleep(1)
```

HTML에서 가격을 추출하는 실습:

``` python
areas = soup.select("body > div")
original_prices = areas[0].find_all(
    "div",
    class_="o-price",
)

print(original_prices[0].get_text().strip())
```

실행 결과:

``` text
27,000원
```

### 코드 해석

- `range(1, 6)` → 1페이지부터 5페이지까지 반복
- URL의 `{page}` → 요청할 페이지 번호
- `time.sleep(1)` → 다음 요청 전 1초 대기
- `class_="o-price"` → class가 `o-price`인 요소 검색
- `original_prices[0]` → 반환된 리스트의 첫 요소 선택
- `get_text().strip()` → 텍스트를 추출하고 양 끝 공백 제거

> **결과 해석:** 페이지별 HTML을 순서대로 가져오되 요청 사이에 간격을 둔다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | `select()` | `find()` | `find_all()` |
| --- | --- | --- | --- |
| 검색 방식 | CSS 선택자 | 태그·속성 조건 | 태그·속성 조건 |
| 반환 | 요소 리스트 | 첫 요소 또는 없음 | 요소 리스트 |
| 텍스트 추출 | 요소를 선택한 뒤 실행 | 반환 요소에서 바로 가능 | 각 요소를 선택하거나 순회 |

------------------------------------------------------------------------

## 6. 주의할 점

- 짧은 시간에 지나치게 많은 요청을 보내지 않는다.
- 반복 요청에는 `time.sleep()` 등으로 간격을 둔다.
- 웹페이지 구조가 바뀌면 기존 추출 코드가 동작하지 않을 수 있다.
- `class`는 Python 키워드이므로 BeautifulSoup 인자에는 `class_`를 사용한다.
- `select()`와 `find_all()`은 리스트를 반환하므로 리스트 전체에 `get_text()`를 바로 호출하지 않는다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `웹 크롤링` | 웹페이지에서 필요한 정보 추출 |
| `HTML` | 웹페이지 구조를 표현하는 문서 |
| `파싱` | HTML 구조를 분석 가능한 형태로 변환 |
| `CSS 선택자` | 태그·id·class·계층으로 요소를 찾는 규칙 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `requests.get(url)` | 웹페이지 요청 |
| `response.text` | HTML 문자열 조회 |
| `BeautifulSoup(..., "html.parser")` | HTML 파싱 |
| `soup.select("#id")` | id를 CSS 선택자로 검색 |
| `find_all(..., class_="name")` | class가 일치하는 모든 요소 검색 |
| `get_text().strip()` | 텍스트 추출과 공백 제거 |
| `time.sleep(1)` | 요청 사이 1초 대기 |

### ⭐ 한 줄 정리

> **requests로 HTML을 가져오고 BeautifulSoup의 선택자와 검색 메소드로 요소를 찾은 뒤 텍스트를 추출한다.**

### 🔖 복습할 내용

- [ ] HTML 응답을 BeautifulSoup 객체로 만들기
- [ ] 반복 페이지 URL 구성하기
- [ ] 요청 사이에 대기 시간 적용하기
- [ ] `select()`, `find()`, `find_all()` 반환값 비교하기
- [ ] `get_text().strip()`으로 텍스트 추출하기
