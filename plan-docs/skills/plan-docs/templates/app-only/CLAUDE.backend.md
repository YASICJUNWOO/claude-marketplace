# CLAUDE.md — backend/

## 기술 스택

<!-- 예시:
- **언어**: Java 21
- **프레임워크**: Spring Boot 3.x
- **빌드 도구**: Gradle (Kotlin DSL)
- **DB**: PostgreSQL 16
- **ORM**: Spring Data JPA + QueryDSL
- **인증**: Spring Security + JWT
- **API 문서**: SpringDoc OpenAPI (Swagger)
- **푸시 알림**: Firebase Cloud Messaging (FCM)
- **테스트**: JUnit 5 + Mockito
-->

## 디렉토리 구조

<!-- 예시:
```
backend/
├── src/
│   ├── main/
│   │   ├── java/com/example/bobfriend/
│   │   │   ├── domain/           # 엔티티, 리포지토리
│   │   │   │   ├── user/
│   │   │   │   ├── match/
│   │   │   │   └── review/
│   │   │   ├── api/              # REST 컨트롤러
│   │   │   ├── service/          # 비즈니스 로직
│   │   │   ├── config/           # 설정 (Security, JPA, FCM 등)
│   │   │   ├── common/           # 공통 (예외 핸들러, DTO 등)
│   │   │   └── infra/            # 외부 연동 (카카오 API, FCM 등)
│   │   └── resources/
│   │       ├── application.yml
│   │       └── db/migration/     # Flyway 마이그레이션
│   └── test/
├── build.gradle.kts
└── CLAUDE.md                     # 이 파일
```
-->

## 빌드/실행 명령어

<!-- 예시:
| 명령어 | 설명 |
|--------|------|
| `./gradlew bootRun` | 개발 서버 실행 |
| `./gradlew build` | 빌드 |
| `./gradlew test` | 전체 테스트 |
| `./gradlew test --tests "*.UserServiceTest"` | 특정 테스트 실행 |
| `./gradlew flywayMigrate` | DB 마이그레이션 |
-->

## 코딩 컨벤션

<!-- 예시:
### 네이밍
- 클래스: PascalCase (예: `MatchRequestService`)
- 메서드/변수: camelCase (예: `findNearbyRequests`)
- 상수: UPPER_SNAKE_CASE (예: `MAX_MATCH_RADIUS_KM`)
- 패키지: lowercase (예: `com.example.bobfriend.domain.match`)

### API 설계
- RESTful URL: `/api/v1/{resource}` (복수형)
- 응답 포맷: `{ "data": ..., "error": null }` 통일
- 에러 응답: `{ "data": null, "error": { "code": "...", "message": "..." } }`
- HTTP 상태코드 준수 (200, 201, 400, 401, 403, 404, 500)

### 코드 구조
- Controller → Service → Repository 레이어 분리
- 비즈니스 로직은 반드시 Service에 작성
- Controller는 요청 검증 + 응답 변환만 담당
- Entity ↔ DTO 변환은 별도 Mapper 또는 정적 팩토리 메서드 사용

### 테스트
- Service 레이어: 단위 테스트 필수
- Controller 레이어: @WebMvcTest 통합 테스트
- Repository 레이어: @DataJpaTest
- 테스트 메서드명: `메서드명_조건_기대결과`
-->
