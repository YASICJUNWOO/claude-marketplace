# SPEC (기술 명세서) — Web

## 1. 페이지 구조 (라우팅)

<!-- 예시:
| 경로 | 페이지명 | 인증 필요 | 설명 |
|------|----------|-----------|------|
| `/` | 랜딩 페이지 | X | 서비스 소개, 로그인 유도 |
| `/login` | 로그인 | X | 소셜 로그인 (카카오, 네이버, 구글) |
| `/signup` | 회원가입 | X | 추가 정보 입력 (닉네임, 음식 취향) |
| `/match` | 매칭 홈 | O | 매칭 요청 + 현재 매칭 상태 |
| `/match/[id]` | 매칭 상세 | O | 매칭 상대 프로필, 식당 추천 |
| `/chat` | 채팅 목록 | O | 매칭된 채팅방 목록 |
| `/chat/[id]` | 채팅방 | O | 1:1 채팅 |
| `/profile` | 내 프로필 | O | 프로필 편집, 매칭 히스토리, 리뷰 |
-->

---

## 2. 페이지별 스펙

### 페이지명: <!-- 예시: 매칭 홈 (`/match`) -->

**컴포넌트 구성:**
<!-- 예시:
- `MatchHeader` — 현재 위치 표시, 반경 설정
- `MatchRequestButton` — "밥친구 찾기" 버튼 (매칭 요청 트리거)
- `MatchStatusCard` — 현재 매칭 대기/진행 상태 표시
- `NearbyUsersMap` — 주변 매칭 대기 유저 수 시각화 (지도)
-->

**사용 API:**
<!-- 예시:
- `POST /api/v1/match-requests` — 매칭 요청 생성
- `GET /api/v1/match-requests/me/active` — 내 활성 매칭 요청 조회
- `WebSocket /ws/match` — 매칭 결과 실시간 수신
-->

**동작 시나리오:**
<!-- 예시:
1. 페이지 진입 시 현재 위치 조회 → 지도에 표시
2. "밥친구 찾기" 클릭 → 매칭 요청 API 호출
3. 매칭 대기 중 → MatchStatusCard에 로딩 애니메이션
4. WebSocket으로 매칭 결과 수신 → 매칭 상세 페이지로 이동
5. 매칭 만료 시 → "다시 찾기" 옵션 표시
-->

---

### 페이지명: <!-- 다음 페이지 ... -->

<!-- 위와 동일한 구조로 각 페이지 작성 -->

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

**에러:**
| 상태코드 | 코드 | 설명 |
|----------|------|------|
| 401 | AUTH_FAILED | 카카오 인증 실패 |
| 400 | INVALID_CODE | 유효하지 않은 인가코드 |
-->

---

### 매칭 API

<!-- 예시:
#### `POST /api/v1/match-requests`
매칭 요청 생성

**Request:**
```json
{
  "latitude": 37.5665,
  "longitude": 126.9780,
  "radiusKm": 1,
  "preferredTime": "2026-02-16T12:00:00"
}
```

**Response (201):**
```json
{
  "data": {
    "id": 1,
    "status": "WAITING",
    "expiredAt": "2026-02-16T12:30:00"
  },
  "error": null
}
```

#### `GET /api/v1/match-requests/me/active`
내 활성 매칭 요청 조회

**Response (200):**
```json
{
  "data": {
    "id": 1,
    "status": "WAITING",
    "latitude": 37.5665,
    "longitude": 126.9780,
    "expiredAt": "2026-02-16T12:30:00"
  },
  "error": null
}
```
-->

---

### 채팅 API

<!-- 예시:
#### `GET /api/v1/chats`
채팅방 목록 조회

#### `GET /api/v1/chats/{chatId}/messages`
채팅 메시지 조회 (페이지네이션)

#### WebSocket `/ws/chat`
실시간 채팅 메시지 송수신
-->

---

### 리뷰 API

<!-- 예시:
#### `POST /api/v1/reviews`
리뷰 작성

#### `GET /api/v1/users/{userId}/reviews`
사용자 리뷰 조회
-->

---

## 변경 이력

| 날짜 | 변경 내용 | 작성자 |
|------|-----------|--------|
| <!-- 예시: 2026-02-16 --> | <!-- 예시: 초안 작성 --> | <!-- 예시: @mason --> |
