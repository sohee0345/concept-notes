---
source:
  - "[[02 정리노트/week04/day12_08.24]]"
---

# Selenium

## 1. 개념

Selenium은 실제 웹 브라우저를 코드로 제어하여 페이지 이동, 요소 탐색, 클릭 같은 동작을 자동화하는 도구이다.

> **핵심:** WebDriver로 브라우저를 열고 요소가 나타날 시간을 고려해 찾아서 상호작용한다.

---

## 2. 쉽게 이해하기

사람이 브라우저에서 주소를 입력하고 버튼을 누르는 행동을 Python 코드가 대신 수행한다.

```text
WebDriver 생성 → 페이지 이동 → 요소 대기·탐색 → 클릭
```

---

## 3. 사용 방법

```python
driver = webdriver.Chrome()
driver.get("https://example.com")
driver.implicitly_wait(5)
driver.find_element(By.NAME, "color_input").click()
```

- `webdriver.Chrome()` → Chrome WebDriver를 생성한다.
- `driver.get()` → 지정한 URL로 이동한다.
- `implicitly_wait(5)` → 요소 탐색 시 최대 5초까지 기다린다.
- `find_element()` → 조건에 맞는 첫 요소를 찾는다.

---

## 4. 예제

`implicitly_wait(5)`는 항상 5초를 멈추는 것이 아니라 요소가 바로 발견되지 않을 때 적용되는 최대 대기 시간이다.

---

## 5. 헷갈리는 개념 비교

|구분|Selenium|requests|
|---|---|---|
|실행|실제 브라우저 제어|HTTP 요청 전송|
|사용|클릭 등 동적 상호작용|정적 응답 수집|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|WebDriver|브라우저를 제어하는 객체|
|요소 탐색|속성이나 선택자로 화면 요소 찾기|
|암시적 대기|요소 탐색에 적용하는 최대 대기 시간|

### 💻 주요 코드

|코드|의미|
|---|---|
|`webdriver.Chrome()`|Chrome 제어 시작|
|`driver.get(url)`|페이지 이동|
|`implicitly_wait(5)`|최대 탐색 대기 시간 설정|
|`find_element(...).click()`|요소를 찾아 클릭|

### ⭐ 한 줄 정리

> **Selenium은 WebDriver로 실제 브라우저의 이동과 요소 상호작용을 자동화한다.**

### 🔖 복습할 내용

- [ ] WebDriver의 역할 설명하기
- [ ] 암시적 대기의 의미 설명하기
- [ ] 요소를 찾아 클릭하는 흐름 작성하기
