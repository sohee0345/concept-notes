---
source:
  - "[[02 정리노트/week07/day29_09.16]]"
---

# PyTorch 모델 체크포인트

## 1. 개념

PyTorch 모델 체크포인트는 학습된 모델의 상태를 파일로 저장해 나중에 추론하거나 학습을 이어갈 수 있게 하는 데이터다. 가장 기본적인 방식은 모델의 파라미터와 버퍼가 담긴 `state_dict()`를 저장하는 것이다.

> **핵심:** `state_dict()`를 불러오려면 저장 당시와 호환되는 모델 구조를 먼저 생성해야 한다.

---

## 2. 쉽게 이해하기

모델 클래스가 빈 기계의 설계도라면 `state_dict()`는 학습을 통해 조정된 모든 다이얼의 현재 위치다.

```text
모델 구조 + 학습된 state_dict → 복원된 모델
```

---

## 3. 사용 방법

```python
torch.save(model.state_dict(), "model.pth")

loaded_model = Model()
state = torch.load("model.pth")
loaded_model.load_state_dict(state)
loaded_model.eval()
```

- `model.state_dict()` → 파라미터와 등록된 버퍼를 이름별로 반환한다.
- `torch.save()` → Python 객체를 파일로 저장한다.
- `torch.load()` → 저장된 객체를 불러온다.
- `load_state_dict()` → 상태를 모델 구조에 적용한다.

---

## 4. 예제

```python
from pathlib import Path

save_dir = Path("models")
save_dir.mkdir(parents=True, exist_ok=True)
save_path = save_dir / "linear_model.pth"

torch.save(model.state_dict(), save_path)

loaded_model = LinearRegressionModel()
loaded_model.load_state_dict(
    torch.load(save_path)
)
loaded_model.eval()

with torch.inference_mode():
    predictions = loaded_model(X_test)
```

불러온 파라미터가 모델 구조의 파라미터 이름과 형태에 맞아야 정상적으로 적용된다.

---

## 5. 헷갈리는 개념 비교

| 구분 | 모델 전체 저장 | `state_dict()` 저장 |
| --- | --- | --- |
| 내용 | 구조와 상태를 함께 직렬화 | 파라미터와 버퍼 저장 |
| 코드 의존성 | 저장 당시 클래스 경로에 크게 의존 | 모델 구조를 코드로 별도 정의 |
| 권장 용도 | 제한적으로 사용 | 일반적인 저장·배포 방식 |

---

## 🟦 핵심 정리

### 💡 주요 개념

체크포인트는 학습 결과를 보존하며, 추론용 저장과 학습 재개용 저장에 필요한 정보 범위가 다르다.

### 💻 주요 코드

| 코드 | 의미 |
| --- | --- |
| `model.state_dict()` | 모델 상태 조회 |
| `torch.save(...)` | 상태 파일 저장 |
| `torch.load(...)` | 상태 파일 읽기 |
| `model.load_state_dict(...)` | 상태를 모델에 적용 |
| `model.eval()` | 복원한 모델을 평가 모드로 전환 |

### ⭐ 한 줄 정리

> **PyTorch 모델은 `state_dict()`를 저장하고 같은 구조의 모델에 다시 적용해 복원한다.**

### 🔖 복습할 내용

- [ ] `state_dict()`에 저장되는 내용 설명하기
- [ ] 저장과 복원 순서 작성하기
- [ ] 추론용 저장과 학습 재개용 체크포인트 구분하기
