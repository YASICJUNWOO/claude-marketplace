# mason-toolkit

Claude Code 플러그인 마켓플레이스 — 아이디어 브레인스토밍부터 프로젝트 문서 생성까지.

## 플러그인 목록

| 플러그인 | 설명 |
|----------|------|
| **brainstorm** | 5단계 아이디어 브레인스토밍 가이드 |
| **plan-docs** | 프로젝트 유형별 문서 자동 생성 (16개 템플릿 번들) |
| **git** | Git 커밋 자동화 및 changelog 생성 (commit, changelog 스킬) |

## 설치

```bash
# 마켓플레이스 추가
/plugin marketplace add mason/claude-marketplace

# 플러그인 설치
/plugin install brainstorm@mason-toolkit
/plugin install plan-docs@mason-toolkit
/plugin install git@mason-toolkit
```

## 사용법

### brainstorm

```bash
/brainstorm:brainstorm 반려동물 커뮤니티 앱
```

5단계로 아이디어를 구체화합니다:
1. 핵심 아이디어 이해
2. 경쟁/기존 솔루션 분석
3. 차별화 기능 브레인스토밍
4. 아이디어 검증 및 도전
5. 최종 정리 (→ plan-docs로 연결)

### plan-docs

```bash
/plan-docs:plan-docs web-only      # 웹 프로젝트
/plan-docs:plan-docs app-only      # 모바일 앱 프로젝트
/plan-docs:plan-docs web-and-app   # 웹 + 앱 프로젝트
```

프로젝트 유형에 맞는 문서를 현재 디렉토리에 생성합니다:
- `docs/PRD.md` — 제품 요구사항 정의서
- `docs/SPEC.md` — 기술 명세서
- `docs/DATA_MODEL.md` — 데이터 모델
- `docs/IMPLEMENTATION_PLAN.md` — 구현 계획
- `CLAUDE.md` — 루트 + 모듈별 Claude Code 컨텍스트

### git

```bash
/git:commit                    # 변경사항 분석 후 자동 커밋
/git:changelog last 2 weeks    # 최근 2주간 changelog 생성
```

- **commit**: 스테이징된 변경사항을 분석하여 conventional commit 메시지를 자동 생성하고 커밋
- **changelog**: 지정 기간의 커밋 히스토리를 분석하여 구조화된 changelog 리포트 생성

## 워크플로우

```
brainstorm → plan-docs
```

1. `brainstorm`으로 아이디어를 구체화
2. 같은 세션에서 `plan-docs`를 실행하면 브레인스토밍 결과를 바탕으로 문서 생성

## 프로젝트 유형

| 유형 | 구조 |
|------|------|
| `web-only` | `backend/` + `web/` |
| `app-only` | `backend/` + `mobile/` |
| `web-and-app` | `backend/` + `web/` + `mobile/` + `shared/` |
