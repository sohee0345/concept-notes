# PCA

## 1. 개념

주성분 분석(Principal Component Analysis, PCA)은 여러 특성의 정보를 데이터 분산이 큰 새로운 축으로 옮겨 적은 수의 특성으로 압축하는 선형 차원 축소 방법이다. 새 축인 주성분들은 서로 직교하며, 앞에 놓인 주성분일수록 더 많은 분산을 설명한다.

> **핵심:** PCA는 원래 특성을 고르는 것이 아니라 여러 특성의 선형 결합으로 새로운 축을 만든다.

---

## 2. 쉽게 이해하기

길쭉한 타원 모양으로 퍼진 점들을 생각하면, 점이 가장 길게 퍼진 방향이 첫 번째 주성분이다. 그 방향에 직각이면서 남은 변화를 가장 잘 나타내는 방향이 두 번째 주성분이다.

```text
원본 데이터
  → 중심 이동
  → 분산이 큰 직교 방향 탐색
  → 주성분에 데이터 투영
  → 일부 주성분만 보존
```

공분산 행렬의 고유벡터는 주성분 방향을, 고유값은 해당 방향의 분산 크기를 나타낸다.

---

## 3. 사용 방법

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)
X_train_reduced = pca.fit_transform(X_train)
X_test_reduced = pca.transform(X_test)

print(pca.explained_variance_ratio_)
```

- `n_components` → 남길 주성분 수
- `fit_transform(X_train)` → 훈련 데이터에서 축을 학습하고 변환
- `transform(X_test)` → 훈련 데이터에서 학습한 같은 축으로 테스트 데이터 변환
- `explained_variance_ratio_` → 각 주성분이 설명하는 분산의 비율

> **핵심:** PCA는 반드시 훈련 데이터로만 학습하고 검증·테스트 데이터에는 `transform()`만 적용한다.

---

## 4. 예제

```python
from sklearn.decomposition import PCA
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import KNeighborsClassifier

model = make_pipeline(
    StandardScaler(),
    PCA(n_components=0.95),
    KNeighborsClassifier(n_neighbors=5),
)
model.fit(X_train, y_train)
score = model.score(X_test, y_test)
```

`n_components=0.95`는 누적 설명 분산이 95% 이상이 되도록 주성분 수를 선택한다. 파이프라인을 사용하면 스케일링과 PCA가 훈련 데이터에만 맞춰져 데이터 누수를 방지하기 쉽다.

---

## 5. 주의할 점

- PCA는 분산이 큰 방향을 중요하게 보므로 특성 단위가 다르면 스케일이 큰 특성이 결과를 지배할 수 있다. 일반적으로 표준화를 먼저 검토한다.
- 주성분은 원래 특성의 조합이므로 개별 특성보다 해석이 어려울 수 있다.
- 많은 분산을 보존해도 예측에 중요한 타깃 정보가 반드시 보존되는 것은 아니다. 최종 모델의 검증 성능도 확인해야 한다.
- 평균 중심화가 필요한 PCA는 큰 희소 행렬에 직접 적용하기 부담스러울 수 있다. 이런 경우 Truncated SVD를 고려한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `주성분` | 데이터 분산을 크게 보존하는 새로운 직교 축 |
| `설명 분산 비율` | 각 주성분이 보존한 전체 분산의 비율 |
| `투영` | 원본 데이터를 주성분 축의 좌표로 바꾸는 과정 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `PCA(n_components=n)` | 주성분 수를 지정해 PCA 생성 |
| `fit_transform()` | 주성분 축을 학습하고 데이터 변환 |
| `explained_variance_ratio_` | 주성분별 설명 분산 비율 확인 |

### ⭐ 한 줄 정리

> **PCA는 데이터의 분산을 많이 보존하는 직교 축을 찾아 원본 특성을 더 적은 수의 주성분으로 압축한다.**

### 🔖 복습할 내용

- [ ] 고유벡터와 고유값이 PCA에서 무엇을 뜻하는가?
- [ ] 설명 분산 비율과 예측 성능을 함께 확인해야 하는 이유는 무엇인가?
- [ ] 훈련 데이터와 테스트 데이터에 `fit_transform()`과 `transform()`을 구분해 적용할 수 있는가?
