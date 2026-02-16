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
│   │   ├── (auth)/               # 인증 관련 라우트 그룹
│   │   │   ├── login/
│   │   │   └── signup/
│   │   ├── (main)/               # 메인 라우트 그룹
│   │   │   ├── match/
│   │   │   ├── chat/
│   │   │   └── profile/
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/               # 공통 컴포넌트
│   │   ├── ui/                   # shadcn/ui 기반 기본 컴포넌트
│   │   └── features/             # 기능별 컴포넌트
│   │       ├── match/
│   │       ├── chat/
│   │       └── profile/
│   ├── hooks/                    # 커스텀 훅
│   ├── lib/                      # 유틸리티, API 클라이언트
│   │   ├── api/                  # API 호출 함수
│   │   └── utils/
│   ├── stores/                   # Zustand 스토어
│   └── types/                    # TypeScript 타입 정의
├── public/
├── package.json
├── tailwind.config.ts
├── tsconfig.json
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
- 컴포넌트: PascalCase 파일명 + default export (예: `MatchCard.tsx`)
- 훅: `use` 접두사 + camelCase (예: `useMatchRequest.ts`)
- 유틸: camelCase (예: `formatDistance.ts`)
- 타입: PascalCase + `type` 키워드 우선 (예: `type MatchRequest = { ... }`)

### 컴포넌트 구조
- Server Component 기본, 필요할 때만 `'use client'`
- Props는 인터페이스 대신 type으로 정의
- 이벤트 핸들러: `handle` + 동사 (예: `handleMatchRequest`)

### API 호출
- `lib/api/` 디렉토리에 도메인별 API 함수 정의
- TanStack Query의 `useQuery` / `useMutation` 래핑
- API 함수는 순수 함수로, React 의존성 없이 작성

### 스타일링
- Tailwind CSS 유틸리티 클래스 사용
- 반복 패턴은 `@apply`가 아닌 컴포넌트로 추출
- 반응형: mobile-first (sm → md → lg)

### 테스트
- 컴포넌트: 사용자 관점 테스트 (Testing Library)
- 훅: renderHook으로 테스트
- 유틸 함수: 순수 단위 테스트
-->
