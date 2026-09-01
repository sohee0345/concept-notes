# Seaborn과 그래프 종류

## 1. 개념

Seaborn은 Matplotlib을 기반으로 만든 시각화 라이브러리로, 데이터 분석용 그래프를 비교적 간단하게 그릴 수 있다.

그래프를 고를 때는 먼저 데이터가 수치형인지 범주형인지 확인해야 한다.

> **핵심:** 어떤 그래프를 그릴지는 데이터 종류와 확인하려는 목적에 따라 결정한다.

---

## 2. 쉽게 이해하기

```text
숫자 ↔ 숫자 관계      → Scatter
시간에 따른 변화       → Line
숫자의 분포            → Histogram
그룹별 분포 비교       → Box
범주별 값 비교         → Bar
밀집 영역 확인         → KDE
```

---

## 3. 사용 방법

```python
import seaborn as sns

sns.scatterplot(...)
sns.lineplot(...)
sns.histplot(...)
sns.boxplot(...)
sns.barplot(...)
```

Seaborn 내장 데이터:

```python
penguins = sns.load_dataset("penguins")
penguins.info()
```

전체 테마:

```python
sns.set_theme(style="darkgrid")
```

---

## 4. 예제

```python
sns.scatterplot(
    data=penguins,
    x="bill_length_mm",
    y="bill_depth_mm"
)
```

두 수치형 변수의 관계를 확인한다.

```python
sns.barplot(
    data=df,
    x="지역",
    y="등록대수"
)
```

범주별 수치 값을 비교한다.

---

## 5. 헷갈리는 개념 비교

| 그래프 | 데이터 | 목적 |
|---|---|---|
| Scatter | 수치형 + 수치형 | 두 변수 관계 |
| Line | 시간/순서 + 수치형 | 변화·추세 |
| Histogram | 수치형 | 분포 |
| Box | 범주형 + 수치형 | 그룹별 분포 비교 |
| Bar | 범주형 + 수치형 | 범주별 값 비교 |
| KDE | 수치형 | 밀도 분포 |

---

## 🟦 핵심 정리

### 💡 주요 개념

- 수치형 → 숫자로 표현되는 데이터
- 범주형 → 종류나 그룹을 나타내는 데이터
- Seaborn → Matplotlib 기반 시각화 라이브러리
- x축 → 기준
- y축 → 확인하고 싶은 값

### 💻 주요 코드

| 코드 | 의미 |
|---|---|
| `sns.scatterplot()` | 두 수치형 변수 관계 |
| `sns.lineplot()` | 변화·추세 |
| `sns.histplot()` | 수치 분포 |
| `sns.boxplot()` | 그룹별 분포 비교 |
| `sns.barplot()` | 범주별 값 비교 |
| `sns.load_dataset()` | 내장 데이터셋 불러오기 |

### ⭐ 한 줄 정리

> **그래프는 데이터 종류와 분석 목적에 맞게 선택해야 한다.**

### 🔖 복습할 내용

- [ ] scatter / line / hist / box / bar 사용 목적
- [ ] 수치형과 범주형 구분
- [ ] x축과 y축 정하는 기준
