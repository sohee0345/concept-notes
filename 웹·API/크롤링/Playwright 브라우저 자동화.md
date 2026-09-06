# Playwright 브라우저 자동화

## 1. 개념

Playwright는 브라우저를 실행하고 페이지 이동, 요소 탐색, 클릭 같은 동작을 코드로 자동화하는 도구이다. 실습에서는 비동기 API로 네이버 로그인 페이지까지 이동했다.

> **핵심:** 브라우저·컨텍스트·페이지를 만들고 `await`로 각 브라우저 작업의 완료를 기다린다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
브라우저 실행
  ↓ 독립 컨텍스트 생성
페이지 탭 생성
  ↓
URL 이동 → 요소 찾기 → 클릭
  ↓
오류 시 스크린샷 → 브라우저 종료
```

> **쉽게 말하면:** 사람이 브라우저에서 하던 이동과 클릭을 Python 코드가 대신 수행하게 하는 것이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
import asyncio
from playwright.async_api import async_playwright

async def main():
    async with async_playwright() as playwright:
        browser = await playwright.chromium.launch(headless=False)
        context = await browser.new_context()
        page = await context.new_page()
        await browser.close()

asyncio.run(main())
```

- `async def` → 비동기 함수 정의
- `await` → 비동기 작업 완료 대기
- `headless=False` → 브라우저 화면 표시
- `new_context()` → 독립된 브라우저 세션 생성
- `new_page()` → 새 페이지 탭 생성

> **핵심:** 브라우저는 작업 성공 여부와 관계없이 마지막에 닫는다.

------------------------------------------------------------------------

## 4. 예제

``` python
async def naver_pay_crawler(playwright):
    browser = await playwright.chromium.launch(headless=False)
    context = await browser.new_context()
    page = await context.new_page()

    try:
        await page.goto("http://www.naver.com")
        await page.wait_for_load_state("networkidle")

        try:
            login_button = await page.wait_for_selector(
                "a.MyView-module__link_login___HpHMW",
                timeout=5000,
            )
            await login_button.click()
        except:
            await page.click("text=로그인")
    except Exception as error:
        print(f"오류 발생: {error}")
        await page.screenshot(path="error_screenshot.png")
    finally:
        await browser.close()
```

### 코드 해석

- `page.goto()` → URL로 이동
- `wait_for_load_state("networkidle")` → 네트워크 요청이 잦아들 때까지 대기
- `wait_for_selector()` → CSS 선택자에 맞는 요소 대기
- `page.click("text=로그인")` → 텍스트로 요소를 찾아 클릭
- `page.screenshot()` → 오류 당시 화면 저장

> **결과 해석:** CSS 선택자를 먼저 사용하고 찾지 못하면 텍스트 선택 방식으로 로그인 버튼을 클릭한다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | requests·BeautifulSoup | Playwright |
| --- | --- | --- |
| 대상 | 응답 HTML 분석 | 실제 브라우저 동작 |
| 주요 작업 | 요청과 파싱 | 이동·대기·클릭 |
| 세션 | 요청 중심 | 브라우저 컨텍스트 사용 |
| 실행 | 일반 함수 | 실습에서는 비동기 API 사용 |

------------------------------------------------------------------------

## 6. 주의할 점

- CSS 클래스 이름은 웹사이트 변경으로 달라질 수 있어 실습에서는 텍스트 선택 방식을 대안으로 사용했다.
- 오류가 발생해도 `finally`에서 브라우저를 닫아 자원을 정리한다.
- 화면이 필요한 로그인 실습에서는 `headless=False`를 사용했다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `Browser` | 자동화할 브라우저 프로세스 |
| `Context` | 독립된 브라우저 세션 |
| `Page` | 브라우저의 페이지 탭 |
| `비동기 실행` | 작업 완료를 기다리며 실행 흐름을 관리하는 방식 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `async_playwright()` | Playwright 비동기 실행 시작 |
| `chromium.launch()` | Chromium 브라우저 실행 |
| `page.goto()` | URL 이동 |
| `wait_for_selector()` | 요소가 나타날 때까지 대기 |
| `page.click()` | 요소 클릭 |
| `asyncio.run(main())` | 비동기 메인 함수 실행 |

### ⭐ 한 줄 정리

> **Playwright는 브라우저 세션과 페이지를 만들고 URL 이동·요소 탐색·클릭을 비동기로 자동화한다.**

### 🔖 복습할 내용

- [ ] Browser·Context·Page 관계 설명하기
- [ ] `async def`, `await`, `asyncio.run()` 흐름 따라가기
- [ ] 선택자 실패 시 대체 클릭 방식 구성하기
- [ ] 오류 시 스크린샷을 저장하고 브라우저 닫기
