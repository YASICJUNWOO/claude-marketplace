# Worktree — Git 워크트리 생성 및 이동

`EnterWorktree` 내장 도구로 워크트리를 생성한 뒤, 브랜치명을 사용자가 원하는 이름으로 변경합니다.

**입력:** `$ARGUMENTS` — `[브랜치명|패턴]`

---

## 인자 파싱 규칙

| 인자 | 필수 | 기본값 | 설명 |
|------|------|--------|------|
| 브랜치명/패턴 | - | 자동 생성 | 브랜치명, 와일드카드 패턴(`fix/*`), 또는 빈 값 |

> 인자가 없으면 현재 대화 컨텍스트를 분석하여 브랜치명을 자동 생성합니다.

---

## 인라인 컨텍스트

- 현재 브랜치: `!git branch --show-current`
- 기존 워크트리 목록: `!git worktree list`
- 로컬 브랜치 목록: `!git branch --list`

---

## 동작 지침

### Step 1: 브랜치명 결정

`$ARGUMENTS`를 다음 3가지 케이스로 분류합니다:

| 케이스 | 판별 조건 | 예시 |
|--------|-----------|------|
| A. 인자 없음 | `$ARGUMENTS`가 비어 있음 | `/git:worktree` |
| B. 구체적 이름 | `*`를 포함하지 않는 문자열 | `/git:worktree feat/login` |
| C. 와일드카드 패턴 | `*`를 포함하는 문자열 | `/git:worktree fix/*` |

#### 케이스 A: 인자 없음

현재 대화 컨텍스트(작업 중인 내용, 이전 메시지 등)를 분석하여 적절한 브랜치명을 생성합니다.

- 형식: `<type>/<kebab-case-description>` (예: `feat/add-login-page`, `fix/header-overflow`)
- 컨텍스트에서 의도를 파악할 수 없으면 사용자에게 브랜치명을 물어봅니다.

#### 케이스 B: 구체적 이름

`$ARGUMENTS`를 그대로 브랜치명으로 사용합니다.

#### 케이스 C: 와일드카드 패턴

`*` 부분을 현재 대화 컨텍스트를 분석하여 적절한 이름으로 채웁니다.

- 예: `fix/*` → `fix/login-null-check` (대화에서 로그인 null 체크 관련 작업 중이라면)
- 컨텍스트에서 의도를 파악할 수 없으면 사용자에게 `*` 부분을 물어봅니다.

### Step 2: 워크트리 생성

`EnterWorktree` 도구를 호출합니다. `name` 파라미터는 생략합니다.

```
EnterWorktree {}
```

### Step 3: 브랜치명 변경

Step 1에서 결정한 브랜치명으로 현재 브랜치를 변경합니다.

```bash
git branch -m <결정된-브랜치명>
```

- 실패 시(동일 이름의 브랜치가 이미 존재하는 등) 에러 메시지를 사용자에게 표시하고 중단합니다.

### Step 4: 결과 출력

```
✓ 워크트리 생성 완료
  브랜치: <branch-name>
  경로:   <worktree-path>
```

---

## 사용 예시

```
/git:worktree
/git:worktree feat/new-feature
/git:worktree fix/*
```
