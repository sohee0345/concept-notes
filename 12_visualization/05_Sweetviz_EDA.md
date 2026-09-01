# Sweetviz를 이용한 EDA

## 1. 개념

Sweetviz는 데이터셋을 자동으로 분석하고 여러 특성을 한눈에 확인할 수 있도록 도와주는 도구이다.

분석할 컬럼을 선택하거나, 숫자로 저장된 데이터를 의미에 따라 범주형으로 강제 지정할 수도 있다.

> **핵심:** 데이터 타입은 저장된 형태뿐 아니라 실제 의미를 보고 판단해야 한다.

---

## 2. 쉽게 이해하기

예를 들어 `survived`가 숫자 `0`, `1`로 저장되어 있어도 실제 의미는

```text
0 → 사망
1 → 생존
```

처럼 종류를 구분하는 값이다.

따라서 숫자라고 해서 항상 수치형 데이터는 아니다.

---

## 3. 사용 방법

```python
import sweetviz as sv

feature_config = sv.FeatureConfig(
    skip="fare",
    force_cat=["survived"]
)
```

- `skip` → 분석에서 제외
- `force_cat` → 범주형으로 강제 처리

필요한 컬럼만 선택:

```python
df = df[[
    "survived",
    "pclass",
    "sex",
    "age"
]]
```

---

## 4. 예제

```python
df = sns.load_dataset("titanic")

feature_config = sv.FeatureConfig(
    skip="fare",
    force_cat=["survived"]
)
```

`survived`는 숫자형 저장이지만 실제로는 생존 여부라는 범주를 나타내므로 범주형으로 처리할 수 있다.

---

## 5. 헷갈리는 개념 비교

| 구분 | 수치형 | 범주형 |
|---|---|---|
| 의미 | 계산 가능한 숫자 | 종류·그룹 구분 |
| 예 | 나이, 요금 | 성별, 지역, 생존 여부 |
| 숫자로 저장 가능 | O | O |

---

## 🟦 핵심 정리

### 💡 주요 개념

- EDA → 데이터 탐색 과정
- Sweetviz → 자동 데이터 탐색 도구
- `skip` → 컬럼 제외
- `force_cat` → 범주형 강제 지정
- 저장 형태와 실제 데이터 의미는 다를 수 있음

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `sv.FeatureConfig()` | Sweetviz 컬럼 설정 |
| `skip="fare"` | 분석에서 컬럼 제외 |
| `force_cat=["survived"]` | 범주형으로 강제 처리 |

### ⭐ 한 줄 정리

> **EDA에서는 데이터가 숫자로 저장되어 있더라도 실제 의미가 범주인지 확인해야 한다.**

### 🔖 복습할 내용

- [ ] 수치형과 범주형 구분
- [ ] `skip`과 `force_cat` 차이
- [ ] 분석할 컬럼을 먼저 선택하는 이유
