---
source:
  - "[[02 정리노트/week02/day06_08.13]]"
---

# Python 표준 라이브러리

## 1. 개념

Python 표준 라이브러리는 Python을 설치할 때 함께 제공되는 기능의 모음이다. 별도 패키지 설치 없이 `import`하여 데이터 집계, 수학 계산, 날짜·시간 처리 등에 사용할 수 있다.

> **핵심:** 표준 라이브러리는 Python에 기본 포함되어 별도 설치 없이 가져와 사용하는 기능이다.

---

## 2. 쉽게 이해하기

Python을 설치하면 함께 들어오는 기본 도구 상자와 같다. 필요한 기능이 있는 모듈을 가져와 사용한다.

```text
Python 설치
  ↓ 표준 라이브러리 포함
모듈 import
  ↓
필요한 기능 사용
```

---

## 3. 사용 방법

```python
from collections import Counter, defaultdict
import math
from datetime import datetime, timedelta
```

- `Counter` → 값별 등장 횟수를 센다.
- `defaultdict` → 없는 키에 접근할 때 기본값을 만든다.
- `math` → 수학 함수와 상수를 제공한다.
- `datetime` → 날짜와 시간을 표현하고 변환한다.
- `timedelta` → 날짜와 시간의 차이를 표현한다.

---

## 4. 예제

```python
from collections import Counter
from datetime import datetime, timedelta
import math

print(Counter(["a", "b", "a"]))
print(math.sqrt(16))
print(datetime.now() + timedelta(days=7))
```

`Counter`는 값을 집계하고 `math.sqrt()`는 제곱근을 계산한다. `timedelta`는 날짜·시간 객체에 기간을 더하거나 뺄 때 사용한다.

---

## 5. 헷갈리는 개념 비교

|구분|`strftime()`|`strptime()`|
|---|---|---|
|변환 방향|날짜·시간 → 문자열|문자열 → 날짜·시간|
|사용|출력 형식 지정|문자열 해석|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|표준 라이브러리|Python에 기본 포함된 기능 모음|
|`collections`|컬렉션 처리를 돕는 모듈|
|`math`|수학 함수와 상수를 제공하는 모듈|
|`datetime`|날짜와 시간을 처리하는 모듈|

### 💻 주요 코드

|코드|의미|
|---|---|
|`Counter(values)`|값별 등장 횟수 계산|
|`defaultdict(int)`|없는 키에 정수 기본값 생성|
|`math.sqrt(16)`|제곱근 계산|
|`datetime.strptime()`|문자열을 날짜·시간으로 변환|

### ⭐ 한 줄 정리

> **Python 표준 라이브러리는 별도 설치 없이 자료 처리, 수학, 날짜·시간 기능을 제공한다.**

### 🔖 복습할 내용

- [ ] 표준 라이브러리와 외부 라이브러리 구분하기
- [ ] `Counter`와 `defaultdict` 비교하기
- [ ] `strftime()`과 `strptime()`의 방향 구분하기
