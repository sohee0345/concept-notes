---
source:
  - "[[02 정리노트/week04/day12_08.24]]"
---

# BeautifulSoup 요소 탐색

## 1. 개념

BeautifulSoup은 HTML 문자열을 태그 구조로 분석하고 CSS 선택자, 태그, 속성을 기준으로 필요한 요소와 텍스트를 찾는 도구이다.

> **핵심:** HTML 구조를 확인한 뒤 select·find·find_all로 요소를 찾고 get_text로 텍스트를 추출한다.

---

## 2. 쉽게 이해하기

HTML 문서를 구조화된 나무로 바꾸고 주소표 역할을 하는 선택자로 원하는 가지를 찾는 과정이다.

```text
HTML → BeautifulSoup → 요소 선택 → 텍스트 추출
```

---

## 3. 사용 방법

- `select()` → CSS 선택자와 일치하는 모든 요소를 찾는다.
- `find()` → 조건에 맞는 첫 요소를 찾는다.
- `find_all()` → 조건에 맞는 모든 요소를 찾는다.
- `get_text(strip=True)` → 내부 태그를 제외하고 공백을 정리한 텍스트를 얻는다.
- `class_` → HTML의 class 속성을 지정한다.

---

## 4. 예제

```python
soup = BeautifulSoup(response.text, "html.parser")
news_sections = soup.select("#newsct")
news_list = news_sections[0].find("ul", class_="sa_list")
titles = [item.get_text(strip=True) for item in news_list.find_all("li")]
```

id로 영역을 찾고 그 안의 목록과 항목을 탐색하여 제목 텍스트를 추출한다.

---

## 5. 헷갈리는 개념 비교

|구분|`select()`|`find()`|`find_all()`|
|---|---|---|---|
|기준|CSS 선택자|태그·속성|태그·속성|
|결과|모든 일치 요소|첫 요소|모든 요소|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|CSS 선택자|HTML 요소를 구조와 속성으로 지정하는 표현|
|요소 탐색|조건에 맞는 태그 찾기|
|텍스트 추출|태그를 제외한 내용 얻기|

### 💻 주요 코드

|코드|의미|
|---|---|
|`soup.select()`|CSS 선택자로 요소 검색|
|`find_all()`|모든 일치 요소 검색|
|`get_text(strip=True)`|텍스트 추출과 공백 정리|

### ⭐ 한 줄 정리

> **BeautifulSoup은 HTML 구조에서 선택자로 요소를 찾고 필요한 텍스트를 추출한다.**

### 🔖 복습할 내용

- [ ] CSS 선택자 기본 형태 설명하기
- [ ] select와 find 계열 비교하기
- [ ] 결과 존재 여부 확인 후 인덱싱하기
