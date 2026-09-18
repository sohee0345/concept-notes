---
source:
  - "[[02 정리노트/week06/day24_09.09]]"
---

# K-means

## 1. 개념

K-means는 K개 중심을 기준으로 가까운 샘플을 할당하고 군집 평균으로 중심을 갱신하는 과정을 반복한다.

> **핵심:** 거리와 평균을 사용하므로 스케일과 이상치에 민감하다.

---

## 2. 쉽게 이해하기

임시 대표점을 놓고 가까운 샘플을 모은 뒤 각 그룹의 평균 위치로 대표점을 옮기는 과정을 반복한다.

```text
중심 선택 → 가까운 중심에 할당 → 평균으로 중심 갱신 → 수렴까지 반복
```

---

## 3. 사용 방법

```python
kmeans = KMeans(n_clusters=3, random_state=42)
labels = kmeans.fit_predict(X_scaled)
centers = kmeans.cluster_centers_
```

- `n_clusters` → 군집 수
- `labels_` → 샘플별 군집 번호
- `cluster_centers_` → 학습된 중심
- `k-means++` → 서로 떨어진 초기 중심 선택

---

## 4. 예제

```python
from sklearn.cluster import KMeans

kmeans = KMeans(n_clusters=3)
kmeans.fit(X)

labels = kmeans.labels_
pred = kmeans.predict(X)
```

MiniBatchKMeans는 작은 미니배치로 중심을 갱신해 대규모 데이터에서 빠르고 메모리 부담이 작지만 결과가 덜 안정적일 수 있다.

---

## 5. 헷갈리는 개념 비교

|구분|K-means|MiniBatchKMeans|
|---|---|---|
|학습 데이터|전체 데이터 반복 사용|미니배치 사용|
|특징|상대적으로 안정적|빠르고 메모리 효율적|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|중심|군집을 대표하는 평균 위치|
|할당|가장 가까운 중심의 군집 선택|
|수렴|중심이나 할당 변화가 멈춘 상태|

### 💻 주요 코드

|코드|의미|
|---|---|
|`KMeans(n_clusters=k)`|K-means 생성|
|`fit_predict()`|학습과 군집 번호 반환|
|`cluster_centers_`|군집 중심 확인|

### ⭐ 한 줄 정리

> **K-means는 가까운 중심에 샘플을 할당하고 평균으로 중심을 반복 갱신한다.**

### 🔖 복습할 내용

- [ ] 중심 갱신 과정 설명하기
- [ ] 스케일링이 필요한 이유 설명하기
- [ ] MiniBatch 방식과 비교하기
