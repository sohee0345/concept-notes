# Feature Engineering

## 1. 개념

Feature Engineering은 기존 데이터를 조합하거나 변환해 모델이 학습할 새로운 Feature를 만드는 과정이다. 새 Feature를 만들면 보통 컬럼 수가 증가한다.

> **핵심:** Train에서 정한 Feature 생성 규칙을 Test에도 똑같이 적용해야 한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

형제·배우자 수와 부모·자녀 수가 따로 있을 때 두 값을 더하면 함께 탑승한 가족 수라는 새로운 정보를 만들 수 있다.

``` text
sibsp + parch
  ↓
family_cnt
```

> **쉽게 말하면:** 이미 가진 재료를 조합해 모델이 이해하기 좋은 새 단서를 만드는 것이다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
train["family_cnt"] = train.apply(
    lambda row: int(row["sibsp"]) + int(row["parch"]),
    axis=1,
)

test["family_cnt"] = test.apply(
    lambda row: int(row["sibsp"]) + int(row["parch"]),
    axis=1,
)
```

- `apply(..., axis=1)` → 각 행을 기준으로 함수 적용
- `family_cnt` → 두 수치형 Feature를 더해 만든 새 Feature
- Train과 Test에 동일한 계산 규칙 적용

> **핵심:** 생성 전후 Shape과 Train·Test의 컬럼 구조를 확인한다.

------------------------------------------------------------------------

## 4. 예제

``` python
train["deck"] = train["deck"].astype(str)
train["deck_who"] = train["deck"] + "_" + train["who"]

test["deck"] = test["deck"].astype(str)
test["deck_who"] = test["deck"] + "_" + test["who"]
```

실행 결과 예시:

``` text
deck = C, who = man → deck_who = C_man
deck = C, who = child → deck_who = C_child
```

### 코드 해석

- `astype(str)` → 문자열 결합이 가능하도록 자료형 변경
- `+ "_" +` → 두 범주를 구분자와 함께 결합
- `deck_who` → 객실 갑판과 승객 유형의 조합을 표현

> **결과 해석:** 각각의 컬럼만 볼 때 드러나지 않던 두 범주의 조합을 하나의 Feature로 표현한다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | 수치형 Feature 조합 | 범주형 Feature 조합 |
| --- | --- | --- |
| 입력 예 | `sibsp`, `parch` | `deck`, `who` |
| 연산 예 | 덧셈 | 문자열 결합 |
| 결과 예 | `family_cnt` | `deck_who` |

------------------------------------------------------------------------

## 6. 주의할 점

- Train과 Test에 서로 다른 생성 규칙을 사용하지 않는다.
- Test Feature를 만들 때 실수로 Train 컬럼을 참조하지 않는다.
- 원본 필기에서는 생성 컬럼 수가 행 수에 비해 지나치게 많지 않도록 확인하고, 일반적인 참고 범위로 행 수의 5% 미만을 언급했다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `Feature Engineering` | 기존 데이터를 조합·변환해 새 Feature를 만드는 과정 |
| `수치형 조합` | 수치 연산으로 새 정보를 생성 |
| `범주형 조합` | 여러 범주의 조합을 새 범주로 표현 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `apply(..., axis=1)` | 각 행에 함수 적용 |
| `astype(str)` | 값을 문자열로 변환 |
| `df["new"] = ...` | 새 Feature 컬럼 생성 |

### ⭐ 한 줄 정리

> **Feature Engineering은 기존 Feature를 조합·변환해 새 단서를 만들고, 같은 규칙을 Train과 Test에 적용하는 과정이다.**

### 🔖 복습할 내용

- [ ] `family_cnt` 생성 코드 다시 작성하기
- [ ] 수치형 조합과 범주형 조합 비교하기
- [ ] Train과 Test에 같은 생성 규칙이 필요한 이유 설명하기
