---
name: changelog
description: >
  Git 커밋 히스토리를 분석하여 피처별로 그룹핑된 변경사항 리포트(changelog)를 생성합니다.
  dev 모드(개발자용 커밋 타입별 분류)와 release 모드(사용자 관점 릴리스 노트)를 지원합니다.
  Use when the user wants to generate a changelog, release notes, commit summary,
  or review what changed in a git branch over a specific date range.
---

# Changelog

**입력:** `$ARGUMENTS` — `<시작일 YYYYMMDD> [종료일 YYYYMMDD] [--branch 브랜치명] [--mode dev|release]`

## 인자 파싱 규칙

| 인자 | 필수 | 기본값 | 설명 |
|------|------|--------|------|
| 시작일 | ✅ | - | YYYYMMDD 형식 |
| 종료일 | - | 오늘 | YYYYMMDD 형식 |
| `--branch` | - | 현재 브랜치 | 대상 브랜치 |
| `--mode` | - | `dev` | `dev` 또는 `release` |

> 위치 인자(positional): 첫 번째 8자리 숫자 → 시작일, 두 번째 8자리 숫자 → 종료일

---

## 동작 지침

### Step 1: 인자 파싱

`$ARGUMENTS`에서 시작일, 종료일, `--branch`, `--mode`를 파싱한다.

- 시작일이 없으면 사용자에게 요청
- 날짜 형식: YYYYMMDD → YYYY-MM-DD로 변환
- `--branch` 미지정 시 `git branch --show-current`로 현재 브랜치 확인

### Step 2: 커밋 수집

```bash
git log --oneline --after="<시작일>" --before="<종료일 +1일>" [브랜치명]
```

- `--before`는 종료일 다음 날로 설정하여 종료일 커밋 포함
- 머지 커밋도 포함하여 전체 흐름 파악

### Step 3: 모드별 출력 생성

## dev 모드 (개발자용)

커밋을 피처 단위로 그룹핑하고, 커밋 타입별로 분류한다.

### 출력 형식

```markdown
# Changelog (dev)
> 브랜치: `{branch}` | 기간: {시작일} ~ {종료일} | 총 {N}건

## 🚀 Features (feat)
### {피처/모듈명}
- {커밋 메시지} (`{short hash}`, {날짜})
- {커밋 메시지} (`{short hash}`, {날짜})

## 🐛 Bug Fixes (fix)
### {피처/모듈명}
- {커밋 메시지} (`{short hash}`, {날짜})

## ♻️ Refactoring (refactor)
- {커밋 메시지} (`{short hash}`, {날짜})

## 🧪 Tests (test)
- {커밋 메시지} (`{short hash}`, {날짜})

## 📝 Docs (docs)
- {커밋 메시지} (`{short hash}`, {날짜})

## 🔧 Chores (chore)
- {커밋 메시지} (`{short hash}`, {날짜})

## 기타
- {분류 불가 커밋} (`{short hash}`, {날짜})
```

### 그룹핑 규칙
- 커밋 메시지의 prefix(`feat:`, `fix:` 등)로 타입 분류
- 같은 모듈/피처에 대한 커밋은 하위 그룹으로 묶음
- 머지 커밋(`merge:`, `Merge branch`)은 컨텍스트 파악에만 사용하고 목록에서 제외

---

## release 모드 (배포/사용자용)

커밋을 분석하여 사용자 관점의 변경사항으로 재작성한다.

### 출력 형식

```markdown
# 릴리스 노트
> 기간: {시작일} ~ {종료일}

## [신규] 새로운 기능
- **{기능명}**: {사용자 관점 설명}
- **{기능명}**: {사용자 관점 설명}

## [변경] 개선된 기능
- **{기능명}**: {무엇이 어떻게 변경되었는지}

## [수정] 버그 수정
- **{현상}**: {해결 내용}
```

### 작성 규칙
- 기술 용어(클래스명, 메서드명, 변수명 등) 제거
- 사용자가 체감할 수 있는 변경만 포함
- `feat` → [신규], `fix` → [수정], 나머지 개선사항 → [변경]
- 사용법이 변경된 경우 간략한 사용 방법 추가
- 커밋 메시지만으로 변경 내용이 불명확한 경우, `git diff`를 읽어 실제 변경 내용을 파악
- 내부 리팩토링, 테스트, 문서 수정 등 사용자에게 영향 없는 변경은 제외

---

## 사용 예시

```
/git:changelog 20260212
/git:changelog 20260212 --mode release
/git:changelog 20260212 20260220 --branch dev
/git:changelog 20260201 20260220 --branch main --mode release
```
