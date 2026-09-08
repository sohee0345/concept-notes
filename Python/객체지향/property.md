# property

## 1. 개념

`property`는 메서드를 속성처럼 사용할 수 있게 하는 기능이다. 조회·수정·삭제 동작을 메서드로 정의하면서 호출할 때는 `()` 없는 속성 문법을 사용한다.

> **핵심:** property는 내부 데이터 접근을 메서드로 관리하면서 외부에는 간단한 속성 문법을 제공한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
student.name 조회 → getter 실행
student.name = 값 → setter 실행
del student.name  → deleter 실행
```

> **쉽게 말하면:** 겉으로는 속성을 다루지만 안에서는 정해 둔 메서드가 실행된다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
@property
def name(self):
    return self.__name

@name.setter
def name(self, value):
    self.__name = value

@name.deleter
def name(self):
    del self.__name
```

- `@property` → 조회 동작 정의
- `@name.setter` → 수정 동작 정의
- `@name.deleter` → 삭제 동작 정의

> **핵심:** 세 메서드는 외부에서 사용할 같은 속성 이름을 기준으로 연결한다.

------------------------------------------------------------------------

## 4. 예제

``` python
class Student:
    def __init__(self, name):
        self.__name = name

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, value):
        self.__name = value

student = Student("홍길동")
student.name = "신사임당"
print(student.name)
```

실행 결과:

``` text
신사임당
```

### 코드 해석

- 대입할 때 setter가 실행된다.
- 조회할 때 getter 역할의 `name()`이 실행된다.

> **결과 해석:** 메서드를 직접 호출하지 않아도 내부 속성의 조회와 수정이 관리된다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| getter | 속성 조회 동작 |
| setter | 속성 수정 동작 |
| deleter | 속성 삭제 동작 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `@property` | getter 정의 |
| `@name.setter` | setter 정의 |
| `@name.deleter` | deleter 정의 |

### ⭐ 한 줄 정리

> **property는 메서드로 속성의 조회·수정·삭제를 관리하게 한다.**

### 🔖 복습할 내용

- [ ] getter와 setter 정의하기
- [ ] 속성 문법으로 property 사용하기
- [ ] deleter 실행 후 조회 결과 확인하기
