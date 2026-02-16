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
│   │   ├── navigation/
│   │   └── App.tsx
│   ├── screens/                  # 스크린 컴포넌트
│   │   ├── auth/
│   │   ├── match/
│   │   ├── chat/
│   │   └── profile/
│   ├── components/               # 앱 전용 컴포넌트
│   │   ├── ui/
│   │   └── features/
│   ├── hooks/
│   ├── lib/
│   │   ├── api/                  # API 호출 (shared/types 사용)
│   │   └── utils/
│   ├── stores/
│   └── types/                    # 앱 전용 타입 (shared/ 외)
├── android/
├── ios/
├── package.json
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
-->

## 코딩 컨벤션

<!-- 예시:
### 네이밍
- 스크린: PascalCase + `Screen` 접미사 (예: `MatchHomeScreen.tsx`)
- 컴포넌트: PascalCase (예: `MatchCard.tsx`)
- 훅: `use` 접두사 (예: `useMatchRequest.ts`)

### 네비게이션 구조
- Auth Stack: 로그인, 회원가입
- Main Tab: 매칭, 채팅, 프로필
- 각 탭 내부는 Stack Navigator

### shared/ 사용
- 공통 타입은 `@shared/types`에서 import
- 공통 상수는 `@shared/constants`에서 import
- 앱 전용 타입만 `src/types/`에 정의

### 플랫폼별 코드
- `Platform.select()` 또는 `.ios.tsx` / `.android.tsx` 확장자 사용
- 웹과 공유할 수 있는 비즈니스 로직은 shared/로 이동

### 테스트
- 스크린: 주요 유저 인터랙션 테스트
- 컴포넌트: 렌더링 + 이벤트 핸들링 테스트
-->
