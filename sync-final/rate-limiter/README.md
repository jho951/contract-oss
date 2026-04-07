# platform-security rate-limiter

`rate-limiter`는 `platform-security`의 요청 속도 제한 구현 레포다.

## 책임

- IP 기준 rate limit
- 사용자 ID 기준 rate limit
- API 키 기준 rate limit
- in-memory 제한
- Redis 기반 분산 제한
- Spring 연동

## 권장 모듈

- `rate-limiter-core`
- `rate-limiter-redis`
- `rate-limiter-spring`
- `rate-limiter-spring-boot-starter`
- `rate-limiter-common-test`

## 모듈 설명

- `rate-limiter-core`: 요청량 제한 규칙과 판단 로직
- `rate-limiter-redis`: Redis 기반 분산 제한
- `rate-limiter-spring`: Spring 어댑터
- `rate-limiter-spring-boot-starter`: 소비 진입점
- `rate-limiter-common-test`: 테스트 지원

## 제외 범위

- 인증 principal 생성
- 정책 엔진 평가
- 감사 저장
- 파일 저장

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)
5. [docs/redis-strategy.md](docs/redis-strategy.md)
