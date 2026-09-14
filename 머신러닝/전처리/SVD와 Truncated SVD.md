# SVD와 Truncated SVD

## 1. 개념

특이값 분해(Singular Value Decomposition, SVD)는 임의의 $m \times n$ 행렬 $A$를 세 행렬의 곱으로 분해하는 방법이다.

$$A=U\Sigma V^T$$

Truncated SVD는 큰 특이값과 이에 대응하는 특이벡터 일부만 남겨 원래 행렬의 주요 구조를 더 낮은 차원으로 근사한다.

> **핵심:** 큰 특이값에 대응하는 성분일수록 원래 행렬의 주요 구조를 더 많이 담는다.

---

## 2. 쉽게 이해하기

SVD는 복잡한 행렬 변환을 방향 변환, 크기 조절, 다시 방향 변환으로 나누어 바라보는 방법이다. 모든 성분을 사용하면 원래 행렬을 복원할 수 있고, 중요한 성분만 사용하면 정보 일부를 보존한 압축 표현을 얻는다.

```text
원본 행렬 A
  → U, Σ, Vᵀ로 분해
  → 큰 특이값 k개 선택
  → 대응하는 벡터만 보존
  → 낮은 차원의 근사 행렬
```

---

## 3. 사용 방법

```python
from sklearn.decomposition import TruncatedSVD

svd = TruncatedSVD(n_components=15, random_state=42)
X_train_reduced = svd.fit_transform(X_train)
X_test_reduced = svd.transform(X_test)

print(svd.explained_variance_ratio_.sum())
```

- `n_components` → 남길 잠재 성분 수
- `fit_transform(X_train)` → 훈련 행렬의 구조를 학습하고 변환
- `transform(X_test)` → 같은 성분 공간으로 테스트 행렬 변환
- `explained_variance_ratio_` → 선택한 성분이 설명하는 분산의 비율

> **핵심:** Truncated SVD는 희소 행렬을 평균 중심화하지 않고 처리할 수 있다.

---

## 4. 예제

```python
import numpy as np

A = np.array([[3.0, 1.0], [1.0, 3.0]])
U, singular_values, Vt = np.linalg.svd(A)
Sigma = np.diag(singular_values)
restored = U @ Sigma @ Vt
```

### 코드 해석

- `np.linalg.svd(A)` → $U$, 특이값, $V^T$를 구한다.
- `np.diag(singular_values)` → 특이값 벡터를 대각 행렬로 만든다.
- `U @ Sigma @ Vt` → 모든 성분을 사용해 원래 행렬을 복원한다.

---

## 5. 헷갈리는 개념 비교

| 구분 | PCA | Truncated SVD |
| --- | --- | --- |
| 중심화 | 평균 중심화를 사용 | 평균 중심화 없이 적용 가능 |
| 희소 행렬 | 중심화로 메모리 부담이 생길 수 있음 | 희소 행렬을 직접 처리 가능 |
| 대표 용도 | 수치형 데이터의 분산 보존 | 문서-단어, 원-핫 인코딩 등 희소 행렬 압축 |
| 공통점 | 선형 성분으로 차원을 축소 | 선형 성분으로 차원을 축소 |

---

## 6. 주의할 점

- 성분을 너무 적게 남기면 중요한 정보까지 손실될 수 있다.
- 설명 분산 비율이 높다고 예측 성능까지 항상 높은 것은 아니다.
- 교차검증을 할 때 SVD를 전체 데이터에 먼저 학습하면 검증 폴드의 정보가 섞일 수 있으므로 파이프라인 안에 포함한다.

---

## 🟦 핵심 정리

### 💡 주요 개념

| 개념 | 의미 |
| --- | --- |
| `특이값` | 각 성분이 행렬 구조에서 차지하는 중요도를 나타내는 크기 |
| `특이벡터` | 행렬의 주요 방향을 나타내는 벡터 |
| `Truncated SVD` | 상위 성분만 남겨 행렬을 저차원으로 근사하는 방법 |

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `np.linalg.svd()` | 행렬을 SVD로 분해 |
| `TruncatedSVD()` | 상위 성분만 사용하는 차원 축소기 생성 |
| `explained_variance_ratio_` | 성분별 설명 분산 비율 확인 |

### ⭐ 한 줄 정리

> **Truncated SVD는 SVD의 큰 특이값에 대응하는 성분만 남겨 희소 행렬의 주요 구조를 저차원으로 압축한다.**

### 🔖 복습할 내용

- [ ] $U$, $\Sigma$, $V^T$의 역할을 설명할 수 있는가?
- [ ] 전체 SVD와 Truncated SVD의 차이를 설명할 수 있는가?
- [ ] 희소 행렬에 Truncated SVD가 적합한 이유를 설명할 수 있는가?
