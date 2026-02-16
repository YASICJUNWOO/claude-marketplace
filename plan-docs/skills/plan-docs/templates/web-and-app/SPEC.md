# SPEC (기술 명세서) — Web + App

## 1. 플랫폼별 화면 구조

### 웹 페이지 구조 (라우팅)

<!-- 예시:
| 경로 | 페이지명 | 인증 필요 | 설명 |
|------|----------|-----------|------|
| `/` | 랜딩 페이지 | X | 서비스 소개, 로그인 유도 |
| `/login` | 로그인 | X | 소셜 로그인 |
| `/signup` | 회원가입 | X | 추가 정보 입력 |
| `/match` | 매칭 홈 | O | 매칭 요청 + 현재 매칭 상태 |
| `/match/[id]` | 매칭 상세 | O | 매칭 상대 프로필 |
| `/chat` | 채팅 목록 | O | 채팅방 목록 |
| `/chat/[id]` | 채팅방 | O | 1:1 채팅 |
| `/profile` | 내 프로필 | O | 프로필 편집, 히스토리 |
-->

### 앱 스크린 구조 (네비게이션)

<!-- 예시:
```
Root Navigator (Stack)
├── Auth Stack
│   ├── LoginScreen
│   └── SignupScreen
└── Main Tab Navigator
    ├── Match Stack
    │   ├── MatchHomeScreen
    │   └── MatchDetailScreen
    ├── Chat Stack
    │   ├── ChatListScreen
    │   └── ChatRoomScreen
    └── Profile Stack
        └── ProfileScreen
```
-->

---

## 2. 화면별 스펙

### 매칭 홈 — 웹: `/match` / 앱: `MatchHomeScreen`

**컴포넌트 구성:**
<!-- 예시:
| 컴포넌트 | 웹 | 앱 | 설명 |
|----------|----|----|------|
| LocationHeader | O | O | 현재 위치 표시, 반경 설정 |
| MatchRequestButton | O | O | "밥친구 찾기" 버튼 |
| MatchStatusCard | O | O | 매칭 대기/진행 상태 |
| NearbyUsersMap | O | O | 주변 매칭 대기 유저 시각화 |
-->

**사용 API:**
<!-- 예시:
- `POST /api/v1/match-requests` — 매칭 요청 생성
- `GET /api/v1/match-requests/me/active` — 내 활성 매칭 요청 조회
- WebSocket `/ws/match` — 매칭 결과 실시간 수신
-->

**플랫폼별 차이:**
<!-- 예시:
| 항목 | 웹 | 앱 |
|------|----|----|
| 위치 권한 | 브라우저 Geolocation API | 네이티브 위치 권한 |
| 지도 라이브러리 | Google Maps JS API | react-native-maps |
| 매칭 알림 | WebSocket → 인앱 토스트 | 푸시 알림 + 인앱 모달 |
-->

---

### 화면명: <!-- 다음 화면 ... -->

<!-- 위와 동일한 구조로 각 화면 작성 -->

---

## 3. 공통 API 엔드포인트

웹과 앱 모두 동일한 백엔드 API를 사용합니다.

### 인증 API

<!-- 예시:
#### `POST /api/v1/auth/login/kakao`
소셜 로그인 (카카오)

**Request:**
```json
{
  "authorizationCode": "string",
  "platform": "WEB" | "APP"
}
```

**Response (200):**
```json
{
  "data": {
    "accessToken": "string",
    "refreshToken": "string",
    "user": {
      "id": 1,
      "nickname": "김밥친",
      "profileImageUrl": "https://..."
    }
  },
  "error": null
}
```
-->

---

### 매칭 API

<!-- 예시:
#### `POST /api/v1/match-requests`
#### `GET /api/v1/match-requests/me/active`
#### `DELETE /api/v1/match-requests/{id}`
-->

---

### 채팅 API

<!-- 예시:
#### `GET /api/v1/chats`
#### `GET /api/v1/chats/{chatId}/messages`
#### WebSocket `/ws/chat`
-->

---

### 리뷰 API

<!-- 예시:
#### `POST /api/v1/reviews`
#### `GET /api/v1/users/{userId}/reviews`
-->

---

### 디바이스 API (앱 전용)

<!-- 예시:
#### `POST /api/v1/devices`
FCM 디바이스 토큰 등록 (앱에서만 호출)

**Request:**
```json
{
  "token": "fcm-device-token",
  "platform": "IOS" | "ANDROID"
}
```
-->

---

## 4. 플랫폼별 차이점 명시

<!-- 예시:
| 기능 | 웹 | 앱 | 비고 |
|------|----|----|------|
| 소셜 로그인 | Redirect 방식 | SDK 방식 (네이티브) | 동일 API, 인증 플로우 다름 |
| 실시간 알림 | WebSocket → 브라우저 알림 | FCM 푸시 알림 | 앱은 백그라운드 알림 가능 |
| 위치 조회 | 브라우저 Geolocation | 네이티브 GPS | 앱이 더 정확 |
| 지도 | Google Maps JS | react-native-maps | 동일 좌표 데이터 |
| 딥링크 | URL 라우팅 | Custom scheme / Universal Link | 앱 미설치 시 웹으로 폴백 |
| 오프라인 | 미지원 | 제한적 지원 (채팅 큐잉) | |
| 결제 | 웹 PG 연동 | 인앱 결제 (IAP) | 수수료 구조 다름 |
-->

---

## 5. 모바일 고유 스펙

### 푸시 알림

<!-- 예시:
| 이벤트 | 알림 내용 | 액션 |
|--------|-----------|------|
| 매칭 성사 | "밥친구를 찾았어요!" | MatchDetailScreen으로 이동 |
| 새 채팅 메시지 | "{nickname}: {message}" | ChatRoomScreen으로 이동 |
-->

### 딥링크

<!-- 예시:
| 딥링크 | 앱 화면 | 웹 폴백 |
|--------|---------|---------|
| `bobfriend://match/{id}` | MatchDetailScreen | `/match/{id}` |
| `bobfriend://chat/{id}` | ChatRoomScreen | `/chat/{id}` |
-->

---

## 변경 이력

| 날짜 | 변경 내용 | 작성자 |
|------|-----------|--------|
| <!-- 예시: 2026-02-16 --> | <!-- 예시: 초안 작성 --> | <!-- 예시: @mason --> |
