---
source:
  - "[[02 정리노트/week06/day22_09.07]]"
---

# Voting과 Stacking

## 1. 개념

Voting은 여러 모델의 클래스나 확률을 직접 결합하고, Stacking은 기본 모델의 예측을 새 Feature로 사용해 메타 모델이 최종 예측을 학습한다.

> **핵심:** Voting은 직접 투표하고 Stacking은 모델 예측을 입력으로 받는 새 모델을 학습한다.

---

## 2. 쉽게 이해하기

Voting은 여러 전문가의 표를 세고 Stacking은 전문가들의 답을 종합하는 별도의 판단자를 훈련한다.

```text
기본 모델들 → 예측
  ├─ Voting: 다수결·확률 평균
  └─ Stacking: 메타 모델 입력
```

---

## 3. 사용 방법

- Hard Voting → 예측 클래스 다수결
- Soft Voting → 클래스 확률 평균
- Stacking → 기본 모델 예측을 메타 Feature로 사용
- 메타 모델 학습에는 검증 폴드 예측을 사용해 누수를 막는다.

---

## 4. 예제

```python
from sklearn.ensemble import VotingClassifier

hp = {
    "estimators": estimators,
    "voting": "soft",
}

voting = VotingClassifier(**hp).fit(X_tr, y_tr)
print(f"훈련용 평가지표: {voting.score(X_tr, y_tr)}")
print(f"테스트용 평가지표: {voting.score(X_te, y_te)}")
```

Soft Voting은 확률을 제공하는 여러 모델의 확률 평균으로 클래스를 선택한다. Stacking은 교차검증에서 얻은 기본 모델 예측으로 메타 모델을 학습한다.

---

## 5. 헷갈리는 개념 비교

|구분|Voting|Stacking|
|---|---|---|
|결합|직접 투표·평균|메타 모델 학습|
|추가 학습|없음|있음|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|Hard Voting|클래스 다수결|
|Soft Voting|클래스 확률 평균|
|Stacking|예측을 Feature로 메타 모델 학습|

### ⭐ 한 줄 정리

> **Voting은 예측을 직접 결합하고 Stacking은 예측을 학습하는 메타 모델을 사용한다.**

### 🔖 복습할 내용

- [ ] Hard와 Soft Voting 비교하기
- [ ] Stacking 흐름 설명하기
- [ ] 검증 폴드 예측이 필요한 이유 설명하기
