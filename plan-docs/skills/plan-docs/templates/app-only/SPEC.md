# SPEC (기술 명세서) — App

## 1. 스크린 구조 (네비게이션)

<!-- 예시:
### 네비게이션 스택/탭 구조

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

| 스크린 | 네비게이터 | 인증 필요 | 설명 |
|--------|-----------|-----------|------|
| LoginScreen | Auth Stack | X | 소셜 로그인 (카카오, 네이버, 구글) |
| SignupScreen | Auth Stack | X | 추가 정보 입력 (닉네임, 음식 취향) |
| MatchHomeScreen | Match Stack | O | 매칭 요청 + 현재 매칭 상태 |
| MatchDetailScreen | Match Stack | O | 매칭 상대 프로필, 식당 추천 |
| ChatListScreen | Chat Stack | O | 매칭된 채팅방 목록 |
| ChatRoomScreen | Chat Stack | O | 1:1 채팅 |
| ProfileScreen | Profile Stack | O | 프로필 편집, 매칭 히스토리, 리뷰 |
-->

---

## 2. 스크린별 스펙

### 스크린명: <!-- 예시: MatchHomeScreen -->

**컴포넌트 구성:**
<!-- 예시:
- `LocationHeader` — 현재 위치 표시, 반경 조절 슬라이더
- `MatchRequestButton` — "밥친구 찾기" 버튼 (매칭 요청 트리거)
- `MatchStatusCard` — 현재 매칭 대기/진행 상태
- `NearbyUsersMap` — 주변 매칭 대기 유저 수 (지도 오버레이)
-->

**사용 API:**
<!-- 예시:
- `POST /api/v1/match-requests` — 매칭 요청 생성
- `GET /api/v1/match-requests/me/active` — 내 활성 매칭 요청 조회
- WebSocket `/ws/match` — 매칭 결과 실시간 수신
-->

**제스처/인터랙션:**
<!-- 예시:
- 반경 슬라이더: 드래그로 0.5~5km 조절
- 매칭 버튼: 탭 → 애니메이션과 함께 매칭 대기 진입
- 매칭 성공 시: 하단에서 슬라이드업 모달로 상대 프로필 표시
- Pull-to-refresh: 상태 새로고침
-->

---

### 스크린명: <!-- 다음 스크린 ... -->

<!-- 위와 동일한 구조로 각 스크린 작성 -->

---

## 3. API 엔드포인트 정의

### 인증 API

<!-- 예시:
#### `POST /api/v1/auth/login/kakao`
소셜 로그인 (카카오)

**Request:**
```json
{
  "authorizationCode": "string"
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

(web-only/SPEC.md의 API 정의와 동일 — 공통 백엔드 사용)
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

## 4. 모바일 고유 스펙

### 푸시 알림

<!-- 예시:
| 이벤트 | 알림 내용 | 액션 |
|--------|-----------|------|
| 매칭 성사 | "밥친구를 찾았어요! 🍚" | MatchDetailScreen으로 이동 |
| 새 채팅 메시지 | "{nickname}: {message}" | ChatRoomScreen으로 이동 |
| 매칭 10분 전 리마인더 | "곧 식사 시간이에요!" | MatchDetailScreen으로 이동 |
| 리뷰 요청 | "식사는 어떠셨나요? 리뷰를 남겨주세요" | ReviewScreen으로 이동 |
-->

### 딥링크

<!-- 예시:
| 딥링크 | 화면 |
|--------|------|
| `bobfriend://match/{matchId}` | MatchDetailScreen |
| `bobfriend://chat/{chatId}` | ChatRoomScreen |
| `bobfriend://profile/{userId}` | ProfileScreen |
-->

### 오프라인 처리

<!-- 예시:
- 네트워크 끊김 시: 상단 배너로 오프라인 상태 안내
- 채팅: 오프라인 메시지 큐잉, 온라인 복귀 시 자동 전송
- 매칭: 오프라인 시 매칭 요청 비활성화
-->

### 권한 요청

<!-- 예시:
| 권한 | 시점 | 사유 |
|------|------|------|
| 위치 (foreground) | 매칭 요청 시 | 주변 밥친구 검색 |
| 알림 | 첫 매칭 성사 시 | 매칭/채팅 알림 수신 |
| 카메라/갤러리 | 프로필 사진 변경 시 | 프로필 이미지 업로드 |
-->

---

## 변경 이력

| 날짜 | 변경 내용 | 작성자 |
|------|-----------|--------|
| <!-- 예시: 2026-02-16 --> | <!-- 예시: 초안 작성 --> | <!-- 예시: @mason --> |
