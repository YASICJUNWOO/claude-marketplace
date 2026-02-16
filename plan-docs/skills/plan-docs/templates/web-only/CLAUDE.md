# CLAUDE.md (루트)

## 프로젝트 개요

<!-- 예시: 밥친구 - 혼밥족 매칭 웹 서비스 -->

## 모노레포 구조

```
프로젝트루트/
├── backend/          # 백엔드 (Spring Boot)
│   └── CLAUDE.md     # → CLAUDE.backend.md 내용 배치
├── web/              # 프론트엔드 (Next.js)
│   └── CLAUDE.md     # → CLAUDE.web.md 내용 배치
├── docs/             # 프로젝트 문서
│   ├── PRD.md
│   ├── SPEC.md
│   ├── DATA_MODEL.md
│   └── IMPLEMENTATION_PLAN.md
├── .env.example
└── CLAUDE.md         # 이 파일
```

## 모듈별 CLAUDE.md

- `backend/CLAUDE.md` — 백엔드 기술 스택, 디렉토리 구조, 빌드/실행 명령어, 코딩 컨벤션
- `web/CLAUDE.md` — 프론트엔드 기술 스택, 디렉토리 구조, 빌드/실행 명령어, 코딩 컨벤션

## 문서 동기화 규칙

**Claude Code는 문서 수정 시 아래 규칙에 따라 연관 문서를 반드시 함께 확인/업데이트해야 합니다.**

1. **PRD.md 기능 변경** → SPEC.md, IMPLEMENTATION_PLAN.md 업데이트
2. **SPEC.md API/화면 변경** → DATA_MODEL.md 정합성 확인, IMPLEMENTATION_PLAN.md 반영
3. **DATA_MODEL.md 변경** → SPEC.md API 스펙 확인/업데이트
4. **IMPLEMENTATION_PLAN.md 마일스톤 변경** → 관련 SPEC.md 범위 확인
5. 어떤 문서든 수정 시, 위 규칙에 따라 연관 문서도 함께 업데이트할 것

## 환경변수 관리

- `.env.example` 파일에 필요한 환경변수 목록 유지
- 실제 값은 `.env.local` (gitignore됨)에 설정
- 새 환경변수 추가 시 `.env.example`에도 반드시 추가

<!-- 예시:
```env
# backend
DATABASE_URL=
JWT_SECRET=
KAKAO_CLIENT_ID=
KAKAO_CLIENT_SECRET=

# web
NEXT_PUBLIC_API_URL=
NEXT_PUBLIC_KAKAO_JS_KEY=
```
-->

## 주요 명령어

<!-- 예시:
| 명령어 | 설명 |
|--------|------|
| `cd backend && ./gradlew bootRun` | 백엔드 실행 |
| `cd web && npm run dev` | 프론트엔드 실행 |
| `cd backend && ./gradlew test` | 백엔드 테스트 |
| `cd web && npm test` | 프론트엔드 테스트 |
-->
