# CLAUDE.md (루트)

## 프로젝트 개요

<!-- 예시: 밥친구 - 혼밥족 매칭 서비스 (웹 + 모바일 앱) -->

## 모노레포 구조

```
프로젝트루트/
├── backend/          # 백엔드 (Spring Boot)
│   └── CLAUDE.md     # → CLAUDE.backend.md 내용 배치
├── web/              # 웹 프론트엔드 (Next.js)
│   └── CLAUDE.md     # → CLAUDE.web.md 내용 배치
├── mobile/           # 모바일 앱 (React Native)
│   └── CLAUDE.md     # → CLAUDE.mobile.md 내용 배치
├── shared/           # 웹 + 앱 공유 코드
│   ├── types/        # 공통 TypeScript 타입
│   ├── constants/    # 공통 상수
│   └── utils/        # 공통 유틸리티
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
- `web/CLAUDE.md` — 웹 프론트엔드 기술 스택, 디렉토리 구조, 빌드/실행 명령어, 코딩 컨벤션
- `mobile/CLAUDE.md` — 모바일 앱 기술 스택, 디렉토리 구조, 빌드/실행 명령어, 코딩 컨벤션

## 공유 코드 관리 규칙 (shared/)

<!-- 예시:
### shared/ 디렉토리 구조
```
shared/
├── types/
│   ├── user.ts          # User, UserProfile 등
│   ├── match.ts         # MatchRequest, Match 등
│   ├── chat.ts          # ChatRoom, Message 등
│   └── api.ts           # ApiResponse, ApiError 등
├── constants/
│   ├── match.ts         # MAX_RADIUS_KM, MATCH_EXPIRE_MINUTES 등
│   └── review.ts        # MIN_RATING, MAX_RATING 등
└── utils/
    ├── date.ts          # 날짜 포맷, 상대 시간 등
    └── validation.ts    # 공통 검증 함수
```
-->

### 규칙
- `shared/`의 코드는 **React/React Native 의존성 없이** 순수 TypeScript로 작성
- 타입, 상수, 유틸리티 함수만 포함 (컴포넌트, 훅 제외)
- `web/`과 `mobile/`에서 `@shared/` 별칭으로 import
- `shared/` 변경 시 web과 mobile 양쪽 빌드 확인 필수

## 문서 동기화 규칙

**Claude Code는 문서 수정 시 아래 규칙에 따라 연관 문서를 반드시 함께 확인/업데이트해야 합니다.**

1. **PRD.md 기능 변경** → SPEC.md, IMPLEMENTATION_PLAN.md 업데이트
2. **SPEC.md API/화면 변경** → DATA_MODEL.md 정합성 확인, IMPLEMENTATION_PLAN.md 반영
3. **DATA_MODEL.md 변경** → SPEC.md API 스펙 확인/업데이트
4. **IMPLEMENTATION_PLAN.md 마일스톤 변경** → 관련 SPEC.md 범위 확인
5. 어떤 문서든 수정 시, 위 규칙에 따라 연관 문서도 함께 업데이트할 것
6. **SPEC.md 플랫폼별 화면 변경** → 다른 플랫폼 대응 화면도 확인 (웹 ↔ 앱 동기화)

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

# mobile
API_BASE_URL=
KAKAO_NATIVE_APP_KEY=
```
-->

## 주요 명령어

<!-- 예시:
| 명령어 | 설명 |
|--------|------|
| `cd backend && ./gradlew bootRun` | 백엔드 실행 |
| `cd web && pnpm dev` | 웹 프론트엔드 실행 |
| `cd mobile && npx expo start` | 모바일 앱 실행 |
| `cd backend && ./gradlew test` | 백엔드 테스트 |
| `cd web && pnpm test` | 웹 테스트 |
| `cd mobile && npm test` | 모바일 앱 테스트 |
-->
