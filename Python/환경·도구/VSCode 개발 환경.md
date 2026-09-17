---
source:
  - "[[02 정리노트/week01/day01_08.06]]"
---

# VSCode 개발 환경

## 1. 개념

Visual Studio Code(VSCode)는 확장 프로그램과 편집기 설정을 조합해 개발 목적에 맞게 구성할 수 있는 코드 편집기이다. Python 개발 지원, Git 이력 확인, 파일 아이콘, PDF 보기 등의 기능을 필요한 만큼 추가할 수 있다.

> **핵심:** VSCode는 확장 프로그램과 편집기 설정을 이용해 목적에 맞는 개발 환경을 구성한다.

---

## 2. 쉽게 이해하기

VSCode가 기본 작업 공간이라면 확장 프로그램은 필요한 기능을 더하는 도구이다. 글꼴과 화면 표시도 설정하여 코드를 읽고 작성하기 편한 환경을 만들 수 있다.

```text
VSCode 설치
  ↓
확장 프로그램 추가
  ↓
개발자용 글꼴 설정
  ↓
코드 작성 환경 완성
```

---

## 3. 사용 방법

- `Python` → Python 코드 작성과 실행을 지원한다.
- `Git Graph` → Git 브랜치와 커밋 흐름을 그래프로 보여 준다.
- `Material Icon Theme` → 파일과 폴더 종류를 아이콘으로 구분한다.
- `vscode-pdf` → VSCode 안에서 PDF 파일을 확인한다.
- `D2Coding ligature` → 코드용 글꼴과 합자 표시를 사용한다.

```json
{
  "editor.fontLigatures": true
}
```

---

## 4. 예제

```text
File → Preferences → Settings
  ↓
font 검색
  ↓
Font Family 앞쪽에 D2Coding ligature 입력
  ↓
Font Ligatures → Edit in settings.json
  ↓
editor.fontLigatures를 true로 변경
```

`editor.fontLigatures`를 `true`로 설정하면 D2Coding ligature의 글꼴 합자 기능이 활성화된다.

---

## 5. 헷갈리는 개념 비교

|구분|확장 프로그램|편집기 설정|
|---|---|---|
|의미|VSCode에 새로운 기능 추가|기존 기능의 동작과 표시 방식 조정|
|예시|Python, Git Graph|Font Family, Font Ligatures|

---

## 🟦 핵심 정리

### 💡 주요 개념

|개념|의미|
|---|---|
|`확장 프로그램`|VSCode에 언어 지원이나 시각화 기능을 추가하는 도구|
|`Font Family`|편집기에서 사용할 글꼴 설정|
|`글꼴 합자`|특정 문자 조합을 하나의 모양으로 표시하는 기능|

### 💻 주요 코드

|코드|의미|
|---|---|
|`"editor.fontLigatures": true`|VSCode 글꼴 합자 기능 활성화|

### ⭐ 한 줄 정리

> **VSCode는 확장 프로그램과 글꼴 설정을 조합해 개발에 필요한 코드 작성 환경으로 구성한다.**

### 🔖 복습할 내용

- [ ] 수업에서 사용한 확장 프로그램의 역할 구분하기
- [ ] VSCode에서 글꼴을 설정하는 흐름 설명하기
- [ ] 글꼴 합자 기능 활성화하기
