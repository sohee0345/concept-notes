---
source:
  - "[[02 정리노트/week05/day19_09.02]]"
---

# train과 test 분리

## 1. 개념

train은 모델과 전처리 기준을 학습하는 데이터이고 test는 학습에 사용하지 않고 최종 성능을 평가하는 데이터이다.

> **핵심:** 데이터를 먼저 분리하고 데이터에서 배우는 모든 과정은 train 안에서 수행한다.

---

## 2. 쉽게 이해하기

train은 연습 문제이고 test는 마지막 시험 문제이다. 시험 문제를 연습 과정에서 보면 평가가 공정하지 않다.

```text
전체 데이터 → train·test 분리 → train 학습 → test 최종 평가
```

---

## 3. 사용 방법

```python
train, test = train_test_split(
    df,
    test_size=0.2,
    random_state=42,
    stratify=df["survived"],
)
```

- `test_size` → test 데이터 비율이다.
- `random_state` → 무작위 분할을 재현하는 시드이다.
- `stratify` → 클래스 비율을 두 데이터에 비슷하게 유지한다.

---

## 4. 예제

```python
x_train = train.drop("target", axis=1)
y_train = train["target"]
x_test = test.drop("target", axis=1)
y_test = test["target"]
```

분할 후 Feature와 Target을 각각 나누어 학습과 평가에 사용한다.

---

## 5. 헷갈리는 개념 비교

|구분|train|test|
|---|---|---|
|목적|전처리·모델 학습|최종 평가|
|통계 계산|가능|학습 기준 계산에 사용하지 않음|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|train|학습용 데이터|
|test|최종 평가용 데이터|
|stratify|클래스 비율을 고려한 분할|
|랜덤 시드|무작위 과정을 재현하는 초기값|

### 💻 주요 코드

|코드|의미|
|---|---|
|`train_test_split()`|데이터 분할|
|`random_state=42`|분할 결과 재현|
|`stratify=y`|클래스 비율 유지|

### ⭐ 한 줄 정리

> **train으로 모든 학습 기준을 만들고 test는 마지막 평가에만 사용한다.**

### 🔖 복습할 내용

- [ ] train과 test 역할 구분하기
- [ ] stratify가 필요한 이유 설명하기
- [ ] 분할 후 Feature와 Target 나누기
