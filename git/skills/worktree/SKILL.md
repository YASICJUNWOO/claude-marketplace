# Worktree — Git 워크트리 생성 및 이동

현재 저장소를 기반으로 워크트리를 생성하고, 작업 디렉토리를 해당 워크트리로 이동합니다.

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

### Step 1: 인자 파싱

`$ARGUMENTS`를 다음 3가지 케이스로 분류합니다:

| 케이스 | 판별 조건 | 예시 |
|--------|-----------|------|
| A. 인자 없음 | `$ARGUMENTS`가 비어 있음 | `/git:worktree` |
| B. 구체적 이름 | `*`를 포함하지 않는 문자열 | `/git:worktree feat/login` |
| C. 와일드카드 패턴 | `*`를 포함하는 문자열 | `/git:worktree fix/*` |

### Step 2: 브랜치명 결정

#### 케이스 A: 인자 없음

현재 대화 컨텍스트(작업 중인 내용, 이전 메시지 등)를 분석하여 적절한 브랜치명을 생성합니다.

- 형식: `<type>/<kebab-case-description>` (예: `feat/add-login-page`, `fix/header-overflow`)
- 컨텍스트에서 의도를 파악할 수 없으면 사용자에게 브랜치명을 물어봅니다.

#### 케이스 B: 구체적 이름

로컬 브랜치 목록에서 해당 이름의 브랜치가 존재하는지 확인합니다.

- **존재함** → 기존 브랜치를 그대로 사용
- **존재하지 않음** → 새 브랜치로 생성

#### 케이스 C: 와일드카드 패턴

`*` 부분을 현재 대화 컨텍스트를 분석하여 적절한 이름으로 채웁니다.

- 예: `fix/*` → `fix/login-null-check` (대화에서 로그인 null 체크 관련 작업 중이라면)
- 컨텍스트에서 의도를 파악할 수 없으면 사용자에게 `*` 부분을 물어봅니다.

### Step 3: 워크트리 경로 결정

브랜치명에서 슬래시(`/`)를 하이픈(`-`)으로 치환하여 디렉토리명을 생성합니다.

```
경로: .worktrees/<sanitized-branch-name>
예: feat/login → .worktrees/feat-login
```

- `.worktrees` 디렉토리가 없으면 자동 생성됩니다.
- 동일 경로에 이미 워크트리가 존재하면 사용자에게 알리고 중단합니다.

### Step 4: 워크트리 생성

#### 기존 브랜치인 경우

```bash
git worktree add ".worktrees/<sanitized-name>" <branch-name>
```

#### 새 브랜치인 경우

```bash
git worktree add -b <branch-name> ".worktrees/<sanitized-name>"
```

- 생성 실패 시 에러 메시지를 사용자에게 표시하고 중단합니다.

### Step 5: 워크트리로 세션 전환

`EnterWorktree` 내장 도구를 실행하여 세션 전체를 워크트리로 전환합니다.

- `EnterWorktree`는 Bash `cd`와 달리 Read, Edit, Glob 등 모든 도구의 작업 디렉토리를 워크트리로 변경합니다.
- `name` 파라미터에 sanitized 브랜치명을 전달합니다.

### Step 6: 결과 출력

```
✓ 워크트리 생성 완료
  브랜치: <branch-name>
  경로:   .worktrees/<sanitized-name>

현재 세션이 워크트리로 전환되었습니다. 모든 도구가 워크트리 경로를 사용합니다.

💡 정리: git worktree remove .worktrees/<sanitized-name>
```

---

## 주의사항

- `git worktree add`로 워크트리를 생성한 뒤 `EnterWorktree` 내장 도구로 세션을 전환합니다. 이렇게 하면 Read, Edit, Glob 등 모든 도구가 워크트리 경로를 사용합니다.
- 세션 종료 시 워크트리가 자동 정리되지 않습니다. 정리 명령(`git worktree remove`)을 안내합니다.
- `.worktrees` 디렉토리가 `.gitignore`에 포함되어 있지 않으면 추가를 권장합니다.

---

## 사용 예시

```
/git:worktree
/git:worktree feat/new-feature
/git:worktree main
/git:worktree fix/*
```
