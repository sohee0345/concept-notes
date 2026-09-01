# Singleton 패턴

## 1. 개념

Singleton은 특정 클래스의 객체를 여러 번 새로 만들지 않고 **하나의 객체만 생성해서 계속 재사용하는 방식**이다.

수업에서는 MySQL 연결 객체를 재사용하기 위해 Singleton을 사용했다.

> **핵심:** Singleton은 객체를 하나만 생성해 여러 곳에서 재사용하는 패턴이다.

---

## 2. 쉽게 이해하기

같은 DB에 접속할 때마다 새로운 연결 객체를 만드는 대신 처음 만든 객체를 계속 쓰는 방식이다.

```text
첫 호출 → 객체 생성
두 번째 호출 → 기존 객체 반환
세 번째 호출 → 기존 객체 반환
```

---

## 3. 사용 방법

```python
class Singleton(type):
    _instances = {}

    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super(Singleton, cls).__call__(*args, **kwargs)

        return cls._instances[cls]
```

---

## 4. 예제

```python
class MySQLDB(metaclass=Singleton):
    ...

db1 = MySQLDB(config)
db2 = MySQLDB(config)

# 같은 객체를 재사용
```

---

## 5. 헷갈리는 개념 비교

| 구분 | 일반 객체 생성 | Singleton |
|---|---|---|
| 여러 번 호출 | 매번 새 객체 | 기존 객체 재사용 |
| 목적 | 독립 객체 생성 | 하나의 공용 객체 유지 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- `_instances` → 생성한 객체 저장
- `__call__()` → 객체 생성 호출을 제어
- `metaclass=Singleton` → Singleton 동작 적용

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `_instances = {}` | 생성된 객체 저장 |
| `if cls not in cls._instances` | 객체 존재 여부 확인 |
| `metaclass=Singleton` | Singleton 메타클래스 적용 |

### ⭐ 한 줄 정리

> **Singleton은 객체를 하나만 생성해 여러 곳에서 재사용하는 패턴이다.**

### 🔖 복습할 내용

- [ ] `_instances` 역할
- [ ] `__call__()`이 호출되는 시점
- [ ] 일반 객체 생성과 Singleton 차이
