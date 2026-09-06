# Selenium 브라우저 자동화

## 1. 개념

Selenium은 WebDriver를 통해 실제 브라우저를 열고 페이지 이동, 요소 검색, 클릭 같은 동작을 자동화하는 도구이다.

> **핵심:** WebDriver로 브라우저를 제어하고 탐색 기준으로 요소를 찾은 뒤 필요한 동작을 실행한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
Chrome WebDriver 생성
  ↓
웹사이트 이동
  ↓
요소가 나타나기를 기다림
  ↓
이름으로 요소 찾기
  ↓
클릭
```

> **쉽게 말하면:** 사람이 브라우저를 열고 버튼을 찾고 누르는 과정을 코드로 실행하는 것이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://example.com")
driver.implicitly_wait(5)
```

- `webdriver.Chrome()` → Chrome WebDriver 생성
- `driver.get()` → URL로 이동
- `implicitly_wait(5)` → 요소를 찾을 때 최대 5초 동안 기다리는 설정
- `By` → 요소를 찾을 기준 제공

> **핵심:** 먼저 페이지로 이동하고 요소가 나타날 시간을 고려한 뒤 탐색한다.

------------------------------------------------------------------------

## 4. 예제

``` python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get(
    "https://www.selenium.dev/selenium/web/linked_image.html"
)
driver.implicitly_wait(5)

driver.find_element(
    By.NAME,
    "color_input",
).click()
```

### 코드 해석

- `By.NAME` → HTML의 `name` 속성을 기준으로 검색한다.
- `find_element()` → 조건에 맞는 요소 하나를 찾는다.
- `click()` → 찾은 요소를 클릭한다.

> **결과 해석:** `name="color_input"`인 요소를 찾아 브라우저에서 클릭한다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | requests·BeautifulSoup | Selenium |
| --- | --- | --- |
| 작업 방식 | HTML 요청과 분석 | 실제 브라우저 제어 |
| 주요 동작 | 파싱·텍스트 추출 | 이동·탐색·클릭 |
| 객체 | Response·BeautifulSoup | WebDriver·WebElement |

------------------------------------------------------------------------

## 6. 주의할 점

- `implicitly_wait(5)`는 무조건 5초 정지하는 것이 아니라 요소 탐색 시 최대 대기 시간을 설정한다.
- 요소의 name이나 페이지 구조가 바뀌면 기존 탐색 코드가 실패할 수 있다.
- 브라우저 자동화가 끝나면 WebDriver 자원을 정리해야 한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `WebDriver` | 브라우저를 제어하는 객체 |
| `WebElement` | 브라우저에서 찾은 HTML 요소 |
| `탐색 기준` | name 등 요소를 찾는 기준 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `webdriver.Chrome()` | Chrome WebDriver 생성 |
| `driver.get(url)` | 페이지 이동 |
| `driver.implicitly_wait(5)` | 요소 탐색 최대 대기 설정 |
| `find_element(By.NAME, value)` | name으로 요소 찾기 |
| `.click()` | 요소 클릭 |

### ⭐ 한 줄 정리

> **Selenium은 WebDriver로 브라우저를 열고 요소를 찾아 클릭하는 동작을 자동화한다.**

### 🔖 복습할 내용

- [ ] WebDriver 생성과 페이지 이동하기
- [ ] `By.NAME`으로 요소 찾기
- [ ] 암시적 대기의 의미 설명하기
