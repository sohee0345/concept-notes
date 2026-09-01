# 예외처리 · assert · raise

## 1. 개념
프로그램 실행 중 발생할 수 있는 오류를 처리하거나, 잘못된 조건을 직접 검사하고 오류를 발생시키는 방법이다.

> **핵심:** 예상 가능한 오류는 `try-except`로 처리하고, 조건 검증에는 `assert`, 직접 오류를 발생시킬 때는 `raise`를 사용한다.

---

## 2. 쉽게 이해하기
```text
코드 실행
  ↓
오류 발생?
 ├─ 아니오 → 정상 실행
 └─ 예 → except에서 처리
```

---

## 3. 사용 방법
```python
try:
    number = int(input("숫자 입력: "))
except ValueError:
    print("숫자를 입력해주세요.")
finally:
    print("종료")
```

- `try` → 오류 가능성이 있는 코드
- `except` → 오류 발생 시 실행
- `finally` → 오류 여부와 상관없이 실행
- `assert 조건, 메시지` → 조건이 거짓이면 `AssertionError`
- `raise` → 원하는 예외를 직접 발생

---

## 4. 예제
```python
age = -1
assert age >= 0, "나이는 0 이상이어야 합니다."
```

실행 결과:
```text
AssertionError: 나이는 0 이상이어야 합니다.
```

---

## 5. 헷갈리는 개념 비교
|구분|`assert`|`raise`|
|---|---|---|
|의미|조건 검증|예외 직접 발생|
|형태|`assert 조건`|`raise 예외종류`|

---

## 🟦 핵심 정리

### 💡 주요 개념
try, except, finally, assert, raise

### 💻 주요 코드
|코드|의미|
|---|---|
|`try/except`|오류 처리|
|`assert 조건`|조건 검증|
|`raise`|예외 발생|

### ⭐ 한 줄 정리
> **예외처리는 오류가 나도 프로그램이 적절하게 대응하도록 만드는 방법이다.**

### 🔖 복습할 내용
- [ ] try-except 흐름
- [ ] finally 역할
- [ ] assert와 raise 차이
