---
source:
  - "[[02 정리노트/week03/day11_08.21]]"
---

# Playwright

## 1. 개념

Playwright는 실제 브라우저를 제어하는 자동화 도구이다. JavaScript 실행, 클릭, 로그인처럼 브라우저 동작 뒤에 내용이 나타나는 동적 페이지 수집에 사용할 수 있다.

> **핵심:** 동적 페이지는 브라우저 상태와 요소 출현을 기다린 뒤 이동·클릭·수집한다.

---

## 2. 쉽게 이해하기

사람이 브라우저를 열고 페이지 이동과 클릭을 하는 과정을 코드가 대신 수행한다.

```text
브라우저 실행 → Context → Page → 이동·대기 → 요소 클릭 → 종료
```

---

## 3. 사용 방법

- `BrowserContext` → 독립적인 브라우저 세션이다.
- `Page` → 브라우저 탭 하나이다.
- `async`, `await` → 비동기 작업 완료를 기다린다.
- `wait_for_selector()` → 요소가 나타날 때까지 기다린다.
- `finally` → 성공과 오류 여부에 관계없이 브라우저를 닫는다.

---

## 4. 예제

```python
async with async_playwright() as playwright:
    browser = await playwright.chromium.launch(headless=False)
    page = await browser.new_page()
    try:
        await page.goto("https://www.naver.com")
        await page.wait_for_load_state("networkidle")
    finally:
        await browser.close()
```

브라우저 화면을 열고 페이지 로딩을 기다린 뒤 작업이 끝나면 항상 종료한다.

---

## 5. 헷갈리는 개념 비교

|구분|requests|Playwright|
|---|---|---|
|대상|정적 응답|브라우저 동작이 필요한 동적 페이지|
|실행|HTTP 요청|실제 브라우저 제어|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|브라우저 자동화|코드로 브라우저 동작을 제어하는 방식|
|비동기|대기 중 다른 작업을 진행할 수 있는 실행 방식|
|선택자|페이지 요소를 찾는 규칙|

### 💻 주요 코드

|코드|의미|
|---|---|
|`asyncio.run(main())`|최상위 비동기 함수 실행|
|`await page.goto()`|페이지 이동 완료 대기|
|`wait_for_selector()`|요소 출현 대기|
|`browser.close()`|브라우저 종료|

### ⭐ 한 줄 정리

> **Playwright는 실제 브라우저를 비동기로 제어하여 동적 페이지의 이동·대기·클릭을 자동화한다.**

### 🔖 복습할 내용

- [ ] BrowserContext와 Page 구분하기
- [ ] `async`와 `await`의 역할 설명하기
- [ ] 오류 시 스크린샷과 브라우저 종료 처리하기
