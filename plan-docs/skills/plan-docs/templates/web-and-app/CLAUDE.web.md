# CLAUDE.md — web/

## 기술 스택

<!-- 예시:
- **프레임워크**: Next.js 15 (App Router)
- **언어**: TypeScript 5.x
- **스타일링**: Tailwind CSS 4
- **상태 관리**: Zustand
- **데이터 페칭**: TanStack Query (React Query)
- **폼**: React Hook Form + Zod
- **UI 컴포넌트**: shadcn/ui
- **테스트**: Vitest + Testing Library
- **패키지 매니저**: pnpm
-->

## 디렉토리 구조

<!-- 예시:
```
web/
├── src/
│   ├── app/                      # Next.js App Router
│   │   ├── (auth)/
│   │   │   ├── login/
│   │   │   └── signup/
│   │   ├── (main)/
│   │   │   ├── match/
│   │   │   ├── chat/
│   │   │   └── profile/
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/               # 웹 전용 컴포넌트
│   │   ├── ui/
│   │   └── features/
│   ├── hooks/
│   ├── lib/
│   │   ├── api/                  # API 호출 (shared/types 사용)
│   │   └── utils/
│   ├── stores/
│   └── types/                    # 웹 전용 타입 (shared/ 외)
├── public/
├── package.json
└── CLAUDE.md                     # 이 파일
```
-->

## 빌드/실행 명령어

<!-- 예시:
| 명령어 | 설명 |
|--------|------|
| `pnpm dev` | 개발 서버 실행 (http://localhost:3000) |
| `pnpm build` | 프로덕션 빌드 |
| `pnpm test` | 테스트 실행 |
| `pnpm lint` | ESLint 실행 |
| `pnpm type-check` | TypeScript 타입 체크 |
-->

## 코딩 컨벤션

<!-- 예시:
### 네이밍
- 컴포넌트: PascalCase (예: `MatchCard.tsx`)
- 훅: `use` 접두사 (예: `useMatchRequest.ts`)
- 유틸: camelCase (예: `formatDistance.ts`)

### 컴포넌트 구조
- Server Component 기본, 필요할 때만 `'use client'`
- Props는 type으로 정의

### shared/ 사용
- 공통 타입은 `@shared/types`에서 import
- 공통 상수는 `@shared/constants`에서 import
- 웹 전용 타입만 `src/types/`에 정의

### 스타일링
- Tailwind CSS 유틸리티 클래스 사용
- 반응형: mobile-first (sm → md → lg)
- 앱과 동일한 디자인 토큰 사용 (색상, 폰트 등)

### 테스트
- 컴포넌트: 사용자 관점 테스트 (Testing Library)
- 훅: renderHook으로 테스트
-->
