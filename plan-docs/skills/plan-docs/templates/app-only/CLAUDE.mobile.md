# CLAUDE.md — mobile/

## 기술 스택

<!-- 예시:
- **프레임워크**: React Native 0.76+ (New Architecture)
- **언어**: TypeScript 5.x
- **네비게이션**: React Navigation 7
- **상태 관리**: Zustand
- **데이터 페칭**: TanStack Query (React Query)
- **스타일링**: NativeWind (Tailwind for RN)
- **푸시 알림**: @react-native-firebase/messaging
- **지도**: react-native-maps
- **테스트**: Jest + React Native Testing Library
- **빌드**: Expo (managed workflow) 또는 bare workflow
-->

## 디렉토리 구조

<!-- 예시:
```
mobile/
├── src/
│   ├── app/                      # 앱 진입점, 네비게이션 설정
│   │   ├── navigation/           # 스택/탭 네비게이터 정의
│   │   └── App.tsx
│   ├── screens/                  # 스크린 컴포넌트
│   │   ├── auth/
│   │   │   ├── LoginScreen.tsx
│   │   │   └── SignupScreen.tsx
│   │   ├── match/
│   │   │   ├── MatchHomeScreen.tsx
│   │   │   └── MatchDetailScreen.tsx
│   │   ├── chat/
│   │   │   ├── ChatListScreen.tsx
│   │   │   └── ChatRoomScreen.tsx
│   │   └── profile/
│   │       └── ProfileScreen.tsx
│   ├── components/               # 공통 컴포넌트
│   │   ├── ui/                   # 기본 UI 컴포넌트 (Button, Card 등)
│   │   └── features/             # 기능별 컴포넌트
│   ├── hooks/                    # 커스텀 훅
│   ├── lib/                      # 유틸리티, API 클라이언트
│   │   ├── api/                  # API 호출 함수
│   │   └── utils/
│   ├── stores/                   # Zustand 스토어
│   └── types/                    # TypeScript 타입 정의
├── android/
├── ios/
├── package.json
├── tsconfig.json
└── CLAUDE.md                     # 이 파일
```
-->

## 빌드/실행 명령어

<!-- 예시:
| 명령어 | 설명 |
|--------|------|
| `npx expo start` | Expo 개발 서버 실행 |
| `npx expo run:ios` | iOS 시뮬레이터 실행 |
| `npx expo run:android` | Android 에뮬레이터 실행 |
| `npm test` | 테스트 실행 |
| `npm run lint` | ESLint 실행 |
| `npm run type-check` | TypeScript 타입 체크 |
-->

## 코딩 컨벤션

<!-- 예시:
### 네이밍
- 스크린: PascalCase + `Screen` 접미사 (예: `MatchHomeScreen.tsx`)
- 컴포넌트: PascalCase (예: `MatchCard.tsx`)
- 훅: `use` 접두사 (예: `useMatchRequest.ts`)
- 네비게이션 파라미터 타입: `ScreenNameParams` (예: `MatchDetailParams`)

### 네비게이션 구조
- Auth Stack: 로그인, 회원가입
- Main Tab: 매칭, 채팅, 프로필
- 각 탭 내부는 Stack Navigator

### 컴포넌트 구조
- 스크린 컴포넌트: 네비게이션 + 데이터 페칭 담당
- Feature 컴포넌트: UI + 인터랙션 담당
- UI 컴포넌트: 순수 프레젠테이션

### API 호출
- `lib/api/` 디렉토리에 도메인별 API 함수 정의
- TanStack Query의 `useQuery` / `useMutation` 래핑
- API 함수는 순수 함수로, React 의존성 없이 작성

### 플랫폼별 코드
- 플랫폼 분기는 `Platform.select()` 또는 `.ios.tsx` / `.android.tsx` 확장자 사용
- 가능하면 플랫폼 공통 코드 유지

### 테스트
- 스크린: 주요 유저 인터랙션 테스트
- 컴포넌트: 렌더링 + 이벤트 핸들링 테스트
- 훅: renderHook으로 테스트
-->
