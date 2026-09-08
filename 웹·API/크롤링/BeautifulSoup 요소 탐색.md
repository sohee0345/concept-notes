# BeautifulSoup 요소 탐색

## 1. 개념

BeautifulSoup은 HTML 문서를 태그 구조로 분석하고 필요한 요소를 찾게 해준다. CSS 선택자를 사용하는 `select()`와 태그·속성 조건을 사용하는 `find()`·`find_all()`을 이용할 수 있다.

> **핵심:** HTML 구조에 맞는 탐색 방법으로 요소를 찾은 뒤 `get_text()`로 텍스트를 꺼낸다.

------------------------------------------------------------------------

## 2. 문서 분석

```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(response.text, "html.parser")
```

`response.text`는 HTML 문자열이고 `soup`은 태그 구조를 탐색할 수 있는 BeautifulSoup 객체이다.

------------------------------------------------------------------------

## 3. 요소 찾기

```python
news_sections = soup.select("#newsct")
first_list = news_sections[0].find("ul", class_="sa_list")
items = first_list.find_all("li")
```

- `select()` → CSS 선택자와 일치하는 모든 요소를 찾는다.
- `find()` → 조건에 맞는 첫 요소를 찾는다.
- `find_all()` → 조건에 맞는 모든 요소를 찾는다.
- `class_` → HTML의 `class` 속성을 지정한다.

`#newsct`의 `#`은 id 선택자를 의미한다.

------------------------------------------------------------------------

## 4. 텍스트 추출

```python
texts = [item.get_text(strip=True) for item in items]
```

`get_text()`는 한 HTML 요소 안의 태그를 제외하고 텍스트를 가져온다. `find_all()` 결과는 여러 요소의 모음이므로 각 요소에 `get_text()`를 적용해야 한다.

------------------------------------------------------------------------

## 5. 주의할 점

- 리스트 결과에 `[0]`으로 접근하기 전에 요소가 실제로 있는지 확인한다.
- Python의 예약어 `class` 대신 `class_`를 사용한다.
- 페이지 구조나 class 이름이 바뀌면 기존 선택자가 더 이상 요소를 찾지 못할 수 있다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| CSS 선택자 | id, class, 계층 구조로 요소를 지정한다. |
| `find_all()` | 조건과 일치하는 모든 요소를 반환한다. |
| `get_text()` | 선택한 요소의 텍스트를 추출한다. |

### ⭐ 한 줄 정리

> **select·find·find_all로 HTML 요소를 찾고 각 요소에 get_text를 적용해 텍스트를 추출한다.**

### 🔖 복습할 내용

- [ ] id와 자식 선택자 작성하기
- [ ] `find()`와 `find_all()`의 결과 차이 설명하기
- [ ] 여러 요소에서 텍스트를 추출하는 반복문 작성하기

