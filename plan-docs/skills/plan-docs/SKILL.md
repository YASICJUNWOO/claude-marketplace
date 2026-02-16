# Plan Docs — 프로젝트 문서 생성

번들된 템플릿을 기반으로 현재 프로젝트 디렉토리에 기획 문서와 CLAUDE.md를 생성합니다.

**입력:** `$ARGUMENTS` — 프로젝트 유형 (`web-only` | `app-only` | `web-and-app`)

---

## 실행 절차

### 1. 프로젝트 유형 확인

`$ARGUMENTS`로 전달된 프로젝트 유형을 확인합니다:

- `web-only` — 웹 프론트엔드 + 백엔드 (`backend/` + `web/`)
- `app-only` — 모바일 앱 + 백엔드 (`backend/` + `mobile/`)
- `web-and-app` — 웹 + 앱 + 공유 백엔드 (`backend/` + `web/` + `mobile/` + `shared/`)

유형이 지정되지 않았거나 유효하지 않으면 사용자에게 선택을 요청합니다.

---

### 2. 번들 템플릿 읽기

이 스킬에 번들된 템플릿 파일들을 읽습니다. 템플릿 경로:

```
templates/
├── common/
│   ├── PRD.md
│   ├── DATA_MODEL.md
│   └── IMPLEMENTATION_PLAN.md
├── web-only/
│   ├── CLAUDE.md
│   ├── CLAUDE.backend.md
│   ├── CLAUDE.web.md
│   └── SPEC.md
├── app-only/
│   ├── CLAUDE.md
│   ├── CLAUDE.backend.md
│   ├── CLAUDE.mobile.md
│   └── SPEC.md
└── web-and-app/
    ├── CLAUDE.md
    ├── CLAUDE.backend.md
    ├── CLAUDE.web.md
    ├── CLAUDE.mobile.md
    └── SPEC.md
```

**읽을 파일:**
- `templates/common/` 의 3개 파일 (모든 유형 공통)
- `templates/{$ARGUMENTS}/` 의 유형별 파일들

---

### 3. 디렉토리 및 문서 생성

현재 프로젝트 디렉토리에 아래 구조를 생성합니다:

#### web-only 인 경우:
```
프로젝트루트/
├── docs/
│   ├── PRD.md                    ← templates/common/PRD.md
│   ├── SPEC.md                   ← templates/web-only/SPEC.md
│   ├── DATA_MODEL.md             ← templates/common/DATA_MODEL.md
│   └── IMPLEMENTATION_PLAN.md    ← templates/common/IMPLEMENTATION_PLAN.md
├── backend/
│   └── CLAUDE.md                 ← templates/web-only/CLAUDE.backend.md
├── web/
│   └── CLAUDE.md                 ← templates/web-only/CLAUDE.web.md
└── CLAUDE.md                     ← templates/web-only/CLAUDE.md
```

#### app-only 인 경우:
```
프로젝트루트/
├── docs/
│   ├── PRD.md                    ← templates/common/PRD.md
│   ├── SPEC.md                   ← templates/app-only/SPEC.md
│   ├── DATA_MODEL.md             ← templates/common/DATA_MODEL.md
│   └── IMPLEMENTATION_PLAN.md    ← templates/common/IMPLEMENTATION_PLAN.md
├── backend/
│   └── CLAUDE.md                 ← templates/app-only/CLAUDE.backend.md
├── mobile/
│   └── CLAUDE.md                 ← templates/app-only/CLAUDE.mobile.md
└── CLAUDE.md                     ← templates/app-only/CLAUDE.md
```

#### web-and-app 인 경우:
```
프로젝트루트/
├── docs/
│   ├── PRD.md                    ← templates/common/PRD.md
│   ├── SPEC.md                   ← templates/web-and-app/SPEC.md
│   ├── DATA_MODEL.md             ← templates/common/DATA_MODEL.md
│   └── IMPLEMENTATION_PLAN.md    ← templates/common/IMPLEMENTATION_PLAN.md
├── backend/
│   └── CLAUDE.md                 ← templates/web-and-app/CLAUDE.backend.md
├── web/
│   └── CLAUDE.md                 ← templates/web-and-app/CLAUDE.web.md
├── mobile/
│   └── CLAUDE.md                 ← templates/web-and-app/CLAUDE.mobile.md
├── shared/
│   ├── types/
│   ├── constants/
│   └── utils/
└── CLAUDE.md                     ← templates/web-and-app/CLAUDE.md
```

---

### 4. 대화 컨텍스트로 내용 채우기

**중요:** 만약 이 세션에서 brainstorm 스킬로 브레인스토밍이 진행된 경우, 그 결과를 활용하여 템플릿의 `<!-- 예시: ... -->` 주석을 **실제 프로젝트 내용**으로 교체합니다.

교체 규칙:
1. `<!-- 예시: ... -->` 주석을 모두 제거
2. 브레인스토밍에서 확정된 내용으로 각 섹션 채우기:
   - **PRD.md**: 프로젝트명, 한 줄 소개, 문제 정의, 타겟 유저, 핵심 기능, 유저 플로우
   - **SPEC.md**: 페이지/스크린 구조, API 엔드포인트, 컴포넌트 구성
   - **DATA_MODEL.md**: 핵심 기능에서 도출된 테이블 스키마, 관계도
   - **IMPLEMENTATION_PLAN.md**: 마일스톤별 구현 계획
   - **CLAUDE.md**: 프로젝트 개요, 기술 스택 (브레인스토밍에서 제안된 것 반영)

만약 브레인스토밍 컨텍스트가 없는 경우, 템플릿을 그대로 복사하되 사용자에게 내용을 채워야 한다고 안내합니다.

---

### 5. 완료 보고

생성된 파일 목록을 정리하여 보고합니다:

```
✓ 프로젝트 문서가 생성되었습니다!

생성된 파일:
  docs/PRD.md
  docs/SPEC.md
  docs/DATA_MODEL.md
  docs/IMPLEMENTATION_PLAN.md
  CLAUDE.md
  backend/CLAUDE.md
  web/CLAUDE.md          (web-only, web-and-app)
  mobile/CLAUDE.md       (app-only, web-and-app)

다음 단계:
  1. 각 문서의 내용을 검토하고 수정하세요
  2. 문서 수정 시 CLAUDE.md의 동기화 규칙을 참고하세요
  3. 구현을 시작하려면 IMPLEMENTATION_PLAN.md의 M1부터 진행하세요
```
