# URL 인코딩 · 디코딩

## 1. 개념
URL에 그대로 사용하기 어려운 문자들을 안전한 형식으로 변환하는 것이 인코딩이고, 원래 문자로 되돌리는 것이 디코딩이다.

> **핵심:** `quote()`로 인코딩하고 `unquote()`로 원래 문자열을 복원한다.

---

## 2. 쉽게 이해하기
```text
한글/특수문자
  ↓ quote()
URL에서 안전한 문자
  ↓ unquote()
원래 문자열
```

---

## 3. 사용 방법
```python
from urllib.parse import quote, unquote

encoded = quote("파이썬")
decoded = unquote(encoded)
```

- `quote()` → 문자열 URL 인코딩
- `unquote()` → 인코딩 문자열 디코딩

---

## 4. 예제
```python
from urllib.parse import quote, unquote

text = "안녕하세요"
encoded = quote(text)
print(unquote(encoded))
```

실행 결과:
```text
안녕하세요
```

---

## 5. 헷갈리는 개념 비교
|구분|인코딩|디코딩|
|---|---|---|
|방향|원문 → URL 안전 형식|URL 형식 → 원문|
|함수|`quote()`|`unquote()`|

---

## 🟦 핵심 정리

### 💡 주요 개념
URL encoding, URL decoding

### 💻 주요 코드
|코드|의미|
|---|---|
|`quote(text)`|URL 인코딩|
|`unquote(text)`|URL 디코딩|

### ⭐ 한 줄 정리
> **URL 인코딩은 문자를 URL에서 안전하게 전달할 수 있는 형태로 바꾸는 과정이다.**

### 🔖 복습할 내용
- [ ] 인코딩이 필요한 이유
- [ ] quote와 unquote 방향
