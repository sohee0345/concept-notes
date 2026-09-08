# Playwright 비동기 브라우저 자동화

## 1. 개념

Playwright는 실제 브라우저를 코드로 제어하는 자동화 도구이다. 페이지 이동, 요소 탐색, 클릭, 대기와 스크린샷 저장을 자동화할 수 있어 동적 웹페이지의 테스트와 데이터 수집에 사용한다.

> **핵심:** Playwright는 브라우저에서 사용자가 수행하는 이동과 클릭을 코드로 재현한다.

------------------------------------------------------------------------

## 2. 객체 흐름

```text
Playwright
  ↓
Browser
  ↓
BrowserContext
  ↓
Page
  ↓
이동·대기·요소 탐색·클릭
```

BrowserContext는 쿠키와 세션을 분리할 수 있는 독립적인 브라우저 환경이고, Page는 그 안의 탭 하나를 나타낸다.

------------------------------------------------------------------------

## 3. 예제

```python
import asyncio
from playwright.async_api import async_playwright


async def main():
    async with async_playwright() as playwright:
        browser = await playwright.chromium.launch(headless=False)
        page = await browser.new_page()

        try:
            await page.goto("http://www.naver.com")
            await page.wait_for_load_state("networkidle")
            await page.click("text=로그인")
        except Exception as error:
            print(f"오류 발생: {error}")
            await page.screenshot(path="error_screenshot.png")
        finally:
            await browser.close()


asyncio.run(main())
```

- `async def` → 비동기 함수를 정의한다.
- `await` → 비동기 작업이 완료될 때까지 현재 함수의 실행을 기다린다.
- `headless=False` → 브라우저 화면을 표시한다.
- `finally` → 실행 결과와 관계없이 브라우저를 닫는다.

------------------------------------------------------------------------

## 4. 요소 탐색과 오류 확인

클래스 이름은 사이트 변경에 따라 달라질 수 있다. 실습에서는 특정 선택자로 요소를 찾지 못하면 표시 텍스트로 다시 찾고, 오류가 발생하면 스크린샷을 저장했다.

```python
try:
    login_button = await page.wait_for_selector(
        "a.MyView-module__link_login___HpHMW",
        timeout=5000,
    )
    await login_button.click()
except Exception:
    await page.click("text=로그인")
```

------------------------------------------------------------------------

## 5. Playwright와 Selenium

| 구분 | Playwright | Selenium |
| --- | --- | --- |
| 공통점 | 실제 브라우저 자동화 | 실제 브라우저 자동화 |
| 적합한 상황 | 최신 웹앱 자동화와 빠른 테스트 | 기존 자동화 코드와 환경 유지 |
| 언어 | Python, JavaScript, Java, C# 등 | 다양한 언어 지원 |

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| Playwright | 브라우저를 코드로 제어하는 자동화 도구이다. |
| BrowserContext | 독립적인 브라우저 세션 환경이다. |
| Page | 브라우저의 탭을 나타낸다. |

### ⭐ 한 줄 정리

> **Playwright의 비동기 API로 브라우저를 열고 페이지 이동과 요소 상호작용을 자동화한다.**

### 🔖 복습할 내용

- [ ] Browser, BrowserContext, Page의 관계 설명하기
- [ ] `async`와 `await`의 역할 구분하기
- [ ] 오류 발생 시 스크린샷을 저장하는 흐름 작성하기

