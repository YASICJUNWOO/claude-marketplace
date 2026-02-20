# Commit — Git 변경사항 분석 후 자동 커밋

세션 내 변경사항 또는 브랜치 전체 변경사항을 분석하여 conventional commit 형식으로 자동 커밋합니다.

**입력:** `$ARGUMENTS` — `[전체] [--confirm] [-m 메시지]`

---

## 인자 파싱 규칙

| 인자 | 필수 | 기본값 | 설명 |
|------|------|--------|------|
| `전체` | - | 세션 변경만 | 브랜치 전체 변경사항을 피처별로 나눠 다중 커밋 |
| `--confirm` | - | 즉시 커밋 | 커밋 전 사용자에게 승인 요청 |
| `-m` | - | 자동 생성 | 커밋 메시지 직접 지정 (따옴표로 감싸기) |

> `전체`는 첫 번째 위치 인자로 판별. `--confirm`과 `-m`은 순서 무관.

---

## 인라인 컨텍스트

- 현재 브랜치: `!git branch --show-current`
- 메인 브랜치: `!git remote show origin 2>/dev/null | grep 'HEAD branch' | awk '{print $NF}' || echo main`

---

## 동작 지침

### Step 1: 인자 파싱

`$ARGUMENTS`에서 다음을 파싱합니다:

- `전체` — 첫 번째 인자가 `전체`이면 전체 모드 활성화
- `--confirm` — 존재하면 커밋 전 승인 모드
- `-m "메시지"` — 존재하면 해당 메시지를 커밋 메시지로 사용

### Step 2: 변경사항 수집

#### 기본 모드 (세션 변경)

```bash
git status
git diff
git diff --cached
```

- 스테이징된 변경과 스테이징 안 된 변경 모두 파악
- 변경사항이 없으면 "커밋할 변경사항이 없습니다" 출력 후 종료

#### 전체 모드

```bash
git diff main...HEAD --stat
git diff main...HEAD
git diff
git diff --cached
```

- 메인 브랜치 대비 현재 브랜치의 전체 변경사항 + 아직 커밋되지 않은 변경사항 분석
- 변경사항을 **피처/모듈 단위**로 그룹핑
- 그룹핑 기준: 관련 파일 경로, 변경 의도, 기능적 연관성

### Step 3: 커밋 메시지 생성

#### `-m` 지정 시

사용자가 제공한 메시지를 그대로 사용합니다.

#### 자동 생성 시

변경사항을 분석하여 **conventional commit** 형식으로 메시지를 생성합니다:

```
<type>[optional scope]: <description>

[optional body]
```

- **type**: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `style`, `perf` 중 적절한 것
- **scope**: 변경 대상 모듈/컴포넌트 (선택)
- **description**: 변경 내용을 간결하게 요약 (한국어 또는 영어, 변경 내용에 맞춰 판단)
- body는 변경이 복잡한 경우에만 추가

**중요: `Co-Authored-By` 라인을 절대 포함하지 않습니다.**

### Step 4: 커밋 실행

#### 기본 모드

1. 변경된 파일을 `git add`로 스테이징 (파일명을 명시적으로 지정)
2. `git commit`으로 커밋
3. `--confirm`이 있으면 커밋 메시지와 대상 파일 목록을 보여주고 사용자 승인 후 실행

#### 전체 모드

1. 피처별로 관련 파일을 그룹핑
2. 각 그룹마다:
   - 해당 파일만 `git add`로 스테이징
   - 그룹에 맞는 커밋 메시지 자동 생성
   - `git commit` 실행
3. `--confirm`이 있으면 전체 커밋 계획(그룹별 파일 목록 + 메시지)을 보여주고 승인 후 실행

### Step 5: 결과 출력

각 커밋에 대해 다음을 출력합니다:

```
✓ <short hash> <커밋 메시지>
  {N} files changed, {+} insertions, {-} deletions
```

전체 모드에서 다중 커밋 시 마지막에 요약:

```
총 {N}건 커밋 완료
```

---

## 주의사항

- 민감한 파일(`.env`, `credentials`, `secret` 등)은 커밋 대상에서 제외하고 경고 출력
- 바이너리 파일이 포함된 경우 사용자에게 알림
- `git add -A`나 `git add .`는 사용하지 않고, 항상 파일을 명시적으로 지정
- 커밋 메시지는 HEREDOC 방식으로 전달하여 특수문자 문제 방지
- `Co-Authored-By` 라인은 절대 포함하지 않음

---

## 사용 예시

```
/git:commit
/git:commit --confirm
/git:commit -m "fix: 로그인 버그 수정"
/git:commit 전체
/git:commit 전체 --confirm
```
