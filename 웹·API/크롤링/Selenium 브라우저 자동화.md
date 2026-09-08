# Selenium 브라우저 자동화

## 1. 개념

Selenium은 실제 웹 브라우저를 코드로 제어하는 자동화 도구이다. URL 이동, 요소 탐색과 클릭 같은 사용자 동작을 자동으로 실행할 수 있다.

> **핵심:** Selenium은 WebDriver를 통해 브라우저와 웹 요소를 제어한다.

------------------------------------------------------------------------

## 2. 실행 흐름

```text
WebDriver 생성
  ↓
웹페이지 이동
  ↓
요소가 나타날 때까지 탐색
  ↓
요소 클릭
```

------------------------------------------------------------------------

## 3. 예제

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://www.selenium.dev/selenium/web/linked_image.html")
driver.implicitly_wait(5)

driver.find_element(By.NAME, "color_input").click()
```

- `webdriver.Chrome()` → Chrome 브라우저를 제어하는 객체를 만든다.
- `driver.get()` → 주소로 이동한다.
- `implicitly_wait(5)` → 요소 탐색 시 최대 5초까지 기다리게 한다.
- `By.NAME` → HTML의 `name` 속성으로 요소를 찾는다.
- `click()` → 찾은 요소를 클릭한다.

------------------------------------------------------------------------

## 4. 주의할 점

- 암시적 대기는 항상 지정 시간만큼 멈추는 `sleep()`과 다르다.
- 요소의 속성이나 페이지 구조가 바뀌면 탐색 조건도 바꿔야 한다.
- 자동화가 끝나면 브라우저 자원을 정리해야 한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| Selenium | 실제 브라우저를 자동으로 제어한다. |
| WebDriver | Python 코드와 브라우저를 연결한다. |
| 요소 탐색 | 속성이나 선택자로 조작할 요소를 찾는다. |

### ⭐ 한 줄 정리

> **Selenium WebDriver로 브라우저를 열고 요소를 찾아 클릭 같은 동작을 자동화한다.**

### 🔖 복습할 내용

- [ ] WebDriver 생성부터 요소 클릭까지 흐름 설명하기
- [ ] `By.NAME`으로 요소 찾기
- [ ] 암시적 대기와 고정 대기의 차이 구분하기

