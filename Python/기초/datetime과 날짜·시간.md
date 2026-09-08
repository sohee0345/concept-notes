# datetime과 날짜·시간

## 1. 개념

`datetime`은 날짜와 시간을 표현하고 형식을 변환하며 계산할 때 사용하는 표준 라이브러리이다. `timedelta`는 두 시점의 차이나 더하고 뺄 시간 간격을 나타낸다.

> **핵심:** datetime은 시점을, timedelta는 시간의 간격을 표현한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
datetime → 2026-08-13 11:16이라는 시점
timedelta → 1일 3시간 30분이라는 간격
```

> **쉽게 말하면:** datetime은 달력과 시계의 값이고 timedelta는 두 시간 사이의 거리이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
from datetime import datetime, timedelta

now = datetime.now()
text = now.strftime("%Y-%m-%d %H:%M")
parsed = datetime.strptime(text, "%Y-%m-%d %H:%M")
after = now + timedelta(days=7)
```

- `datetime.now()` → 현재 날짜와 시간
- `strftime()` → datetime을 문자열로 변환
- `strptime()` → 문자열을 datetime으로 변환
- `timedelta()` → 날짜·시간 간격 생성

> **핵심:** 문자열과 datetime을 변환할 때 형식 문자열을 데이터와 맞춰야 한다.

------------------------------------------------------------------------

## 4. 예제

``` python
text = "2026-08-13 11:16"
value = datetime.strptime(text, "%Y-%m-%d %H:%M")
print(value.year)
print(value + timedelta(days=1))
```

실행 결과:

``` text
2026
2026-08-14 11:16:00
```

### 코드 해석

- `strptime()`은 문자열을 날짜·시간 객체로 해석한다.
- `timedelta(days=1)`을 더해 하루 뒤 시점을 만든다.

> **결과 해석:** 변환된 datetime에서는 구성 요소 조회와 날짜 계산이 가능하다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | `strftime()` | `strptime()` |
| --- | --- | --- |
| 변환 | datetime → 문자열 | 문자열 → datetime |
| 결과 | `str` | `datetime` |

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `datetime` | 날짜와 시간의 한 시점 |
| `timedelta` | 날짜와 시간의 간격 |
| 형식 문자열 | 날짜 문자열의 구성 지정 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `datetime.now()` | 현재 시각 생성 |
| `strftime()` | 문자열로 변환 |
| `strptime()` | datetime으로 변환 |

### ⭐ 한 줄 정리

> **datetime으로 시점을 표현하고 timedelta로 날짜와 시간의 차이를 계산한다.**

### 🔖 복습할 내용

- [ ] 현재 날짜와 시간 조회하기
- [ ] 두 형식 변환 함수의 방향 구분하기
- [ ] timedelta를 더하고 빼기
