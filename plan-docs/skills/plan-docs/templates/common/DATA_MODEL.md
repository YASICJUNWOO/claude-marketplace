# DATA MODEL

## 개요

<!-- 예시: 밥친구 서비스의 데이터 모델 정의. PostgreSQL 기반. -->

---

## 1. 테이블 스키마

### 테이블명: `테이블명`
<!-- 예시:
### 테이블명: `users`

| 컬럼명 | 타입 | 제약조건 | 설명 |
|--------|------|----------|------|
| id | BIGINT | PK, AUTO_INCREMENT | 사용자 고유 ID |
| email | VARCHAR(255) | UNIQUE, NOT NULL | 이메일 |
| nickname | VARCHAR(50) | NOT NULL | 닉네임 |
| profile_image_url | VARCHAR(500) | NULLABLE | 프로필 이미지 URL |
| phone_number | VARCHAR(20) | UNIQUE, NOT NULL | 휴대폰 번호 |
| food_preferences | JSONB | NULLABLE | 음식 취향 (한식, 양식 등) |
| manner_score | DECIMAL(3,2) | DEFAULT 5.0 | 매너 점수 (1.0~5.0) |
| status | VARCHAR(20) | DEFAULT 'ACTIVE' | ACTIVE / SUSPENDED / DELETED |
| created_at | TIMESTAMP | NOT NULL | 가입일시 |
| updated_at | TIMESTAMP | NOT NULL | 수정일시 |

### 테이블명: `match_requests`

| 컬럼명 | 타입 | 제약조건 | 설명 |
|--------|------|----------|------|
| id | BIGINT | PK, AUTO_INCREMENT | 매칭 요청 ID |
| user_id | BIGINT | FK → users.id, NOT NULL | 요청 사용자 |
| latitude | DECIMAL(10,8) | NOT NULL | 위도 |
| longitude | DECIMAL(11,8) | NOT NULL | 경도 |
| radius_km | INT | DEFAULT 1 | 매칭 반경 (km) |
| preferred_time | TIMESTAMP | NOT NULL | 희망 식사 시간 |
| status | VARCHAR(20) | DEFAULT 'WAITING' | WAITING / MATCHED / EXPIRED / CANCELLED |
| created_at | TIMESTAMP | NOT NULL | 요청일시 |
| expired_at | TIMESTAMP | NOT NULL | 만료일시 |

### 테이블명: `matches`

| 컬럼명 | 타입 | 제약조건 | 설명 |
|--------|------|----------|------|
| id | BIGINT | PK, AUTO_INCREMENT | 매칭 ID |
| request_id_1 | BIGINT | FK → match_requests.id | 매칭 요청 1 |
| request_id_2 | BIGINT | FK → match_requests.id | 매칭 요청 2 |
| status | VARCHAR(20) | DEFAULT 'PENDING' | PENDING / CONFIRMED / COMPLETED / CANCELLED |
| created_at | TIMESTAMP | NOT NULL | 매칭일시 |

### 테이블명: `reviews`

| 컬럼명 | 타입 | 제약조건 | 설명 |
|--------|------|----------|------|
| id | BIGINT | PK, AUTO_INCREMENT | 리뷰 ID |
| match_id | BIGINT | FK → matches.id | 매칭 ID |
| reviewer_id | BIGINT | FK → users.id | 작성자 |
| reviewee_id | BIGINT | FK → users.id | 대상자 |
| rating | INT | NOT NULL, CHECK(1~5) | 평점 |
| comment | TEXT | NULLABLE | 코멘트 |
| created_at | TIMESTAMP | NOT NULL | 작성일시 |
-->

---

## 2. 테이블 관계도

<!-- 예시:
```
users (1) ──── (N) match_requests
match_requests (1) ──── (N) matches (via request_id_1, request_id_2)
matches (1) ──── (N) reviews
users (1) ──── (N) reviews (via reviewer_id, reviewee_id)
```

```
┌──────────┐       ┌─────────────────┐       ┌──────────┐
│  users   │1────N│ match_requests  │N────1│  matches │
└──────────┘       └─────────────────┘       └──────────┘
     │1                                            │1
     │                                             │
     │N                                            │N
┌──────────┐                                 ┌──────────┐
│ (다른    │                                 │ reviews  │
│  테이블) │                                 └──────────┘
└──────────┘
```
-->

---

## 3. 인덱스 전략

<!-- 예시:
| 테이블 | 인덱스명 | 컬럼 | 타입 | 이유 |
|--------|----------|------|------|------|
| users | idx_users_email | email | UNIQUE | 로그인 시 이메일 조회 |
| users | idx_users_phone | phone_number | UNIQUE | 본인 인증 조회 |
| match_requests | idx_mr_status_location | (status, latitude, longitude) | COMPOSITE | 주변 매칭 요청 조회 |
| match_requests | idx_mr_user_status | (user_id, status) | COMPOSITE | 사용자별 활성 요청 조회 |
| matches | idx_matches_status | status | BTREE | 상태별 매칭 조회 |
| reviews | idx_reviews_reviewee | reviewee_id | BTREE | 사용자 평점 집계 |
-->

---

## 4. 마이그레이션 이력

| 버전 | 날짜 | 설명 | 작성자 |
|------|------|------|--------|
| <!-- 예시: V1 --> | <!-- 예시: 2026-02-16 --> | <!-- 예시: 초기 스키마 생성 (users, match_requests, matches, reviews) --> | <!-- 예시: @mason --> |

---

## 변경 이력

| 날짜 | 변경 내용 | 작성자 |
|------|-----------|--------|
| <!-- 예시: 2026-02-16 --> | <!-- 예시: 초안 작성 --> | <!-- 예시: @mason --> |
