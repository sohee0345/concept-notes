---
source:
  - "[[02 정리노트/week01/day02_08.07]]"
---

# Enum

## 1. 개념

`enum.Enum`은 이름이 있는 값의 집합을 정의하는 열거형이다. 서로 관련된 고정 값을 하나의 타입으로 묶고 멤버 이름을 통해 각 값에 접근한다.

> **핵심:** Enum은 관련된 고정 값을 이름 있는 멤버의 집합으로 표현한다.

---

## 2. 쉽게 이해하기

무지개 색처럼 미리 정해진 값의 목록에 이름표를 붙여 하나의 그룹으로 만든다고 생각할 수 있다.

```text
RAINBOW 열거형
  ↓
RED, ORANGE 등의 멤버
  ↓
RAINBOW.RED.value로 실제 값 조회
```

---

## 3. 사용 방법

```python
import enum

class RAINBOW(enum.Enum):
    RED = "빨강"
    ORANGE = "주황"
```

- `import enum` → 열거형을 정의하는 모듈을 가져온다.
- `class RAINBOW(enum.Enum)` → `Enum`을 상속해 열거형을 정의한다.
- `RED` → 열거형 멤버의 이름이다.
- `.value` → 멤버에 저장된 실제 값을 가져온다.

---

## 4. 예제

```python
import enum

class RAINBOW(enum.Enum):
    RED = "빨강"
    ORANGE = "주황"
    YELLOW = "노랑"

print(RAINBOW.RED.value)
```

실행 결과:

```text
빨강
```

`RAINBOW.RED`로 멤버를 선택하고 `.value`로 실제 문자열을 조회한다.

---

## 5. 헷갈리는 개념 비교

|구분|대문자 변수|Enum 멤버|
|---|---|---|
|의미|변경하지 않을 값이라는 이름 관례|이름 있는 값의 집합에 포함된 멤버|
|값 변경|Python이 막지 않음|멤버 값 변경 시 오류 발생|
|접근 예시|`PI`|`RAINBOW.RED.value`|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`Enum`|이름이 있는 값의 집합을 정의하는 열거형|
|`멤버`|열거형 안에 정의된 이름 있는 값|
|`.value`|멤버의 실제 값에 접근하는 속성|

### 💻 주요 코드

|코드|의미|
|---|---|
|`class RAINBOW(enum.Enum)`|Enum을 상속한 열거형 정의|
|`RAINBOW.RED.value`|RED 멤버의 실제 값 조회|

### ⭐ 한 줄 정리

> **Enum은 관련된 고정 값을 이름 있는 멤버로 묶고 `.value`로 실제 값에 접근하는 열거형이다.**

### 🔖 복습할 내용

- [ ] Enum이 필요한 이유 설명하기
- [ ] Enum 멤버와 실제 값 구분하기
- [ ] 대문자 변수와 Enum 멤버 비교하기
