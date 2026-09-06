# One-Hot Encoding

## 1. 개념

One-Hot Encoding은 범주형 값을 범주별 이진 컬럼으로 변환하는 방법이다. 문자열 범주를 모델이 사용할 수 있는 수치 형태로 바꾼다.

> **핵심:** Encoder는 Train 범주로 학습하고 Train과 Test에 같은 컬럼 구조를 만들어야 한다.

------------------------------------------------------------------------

## 2. 쉽게 이해하기

``` text
sex = male / female
  ↓ One-Hot Encoding
sex_male | sex_female
    1     |     0
    0     |     1
```

> **쉽게 말하면:** 하나의 범주 컬럼을 각 선택지에 해당하는지 표시하는 여러 개의 0·1 컬럼으로 펼친다.

------------------------------------------------------------------------

## 3. 사용 방법

``` python
import category_encoders as ce

encoder = ce.OneHotEncoder(use_cat_names=True)

encoder.fit(x_train_str[col].astype("category"))
train_encoded = encoder.transform(
    x_train_str[col].astype("category")
)
test_encoded = encoder.transform(
    x_test_str[col].astype("category")
)
```

- `use_cat_names=True` → 생성 컬럼명에 범주 이름 사용
- `fit()` → Train 범주 학습
- `transform()` → 같은 기준으로 데이터 변환

> **핵심:** Test에는 `fit()`하지 않고 Train에서 학습한 Encoder를 사용한다.

------------------------------------------------------------------------

## 4. 예제

``` python
x_train_enc, x_test_enc = transform_encoding(
    EncodingType.OneHot,
    x_train_str,
    x_test_str,
)
```

실행 결과:

``` text
x_train_enc.shape → (712, 19)
x_test_enc.shape  → (179, 19)
```

### 코드 해석

- 문자열 Feature별로 Train에서 Encoder 학습
- Train과 Test를 같은 Encoder로 변환
- 변환된 컬럼을 `concat(..., axis=1)`로 누적

> **결과 해석:** Train과 Test에 같은 19개의 인코딩 Feature가 생성되었다.

------------------------------------------------------------------------

## 5. 헷갈리는 개념 비교

| 구분 | 원본 범주형 컬럼 | One-Hot 결과 |
| --- | --- | --- |
| 값 | 문자열·범주 | 0과 1 |
| 컬럼 수 | 하나 | 범주에 따라 여러 개 |
| 모델 입력 | 그대로 사용하기 어려울 수 있음 | 수치형 Feature로 사용 가능 |

------------------------------------------------------------------------

## 6. 주의할 점

- Train과 Test를 서로 다른 기준으로 학습하면 컬럼 구조가 달라질 수 있다.
- 열 방향 결합 전 DataFrame 인덱스를 맞춰야 한다.
- 인코딩 후 Train과 Test의 컬럼 수가 같은지 확인한다.

------------------------------------------------------------------------

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `One-Hot Encoding` | 범주를 여러 이진 컬럼으로 변환 |
| `Encoder fit` | Train 범주 학습 |
| `Encoder transform` | 학습된 범주 기준 적용 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `ce.OneHotEncoder()` | Encoder 생성 |
| `encoder.fit()` | Train 범주 학습 |
| `encoder.transform()` | 데이터 변환 |
| `pd.concat(..., axis=1)` | 인코딩 컬럼 결합 |

### ⭐ 한 줄 정리

> **One-Hot Encoding은 Train에서 학습한 범주 기준으로 Train과 Test를 같은 이진 컬럼 구조로 변환한다.**

### 🔖 복습할 내용

- [ ] 범주 하나가 여러 컬럼으로 바뀌는 과정 설명하기
- [ ] Train에만 fit해야 하는 이유 설명하기
- [ ] 인코딩 후 Train·Test 열 수 검증하기
