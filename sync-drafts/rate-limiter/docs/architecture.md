# Architecture

`rate-limiter`는 요청량을 제어하는 플랫폼 구현 레포다.

## 설계 원칙

- rate limit은 플랫폼 책임이다.
- 서비스는 제한 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.
- Spring wiring은 adapter layer에 둔다.

## 구성 요소

- `rate-limiter-core`: rate limit 핵심 로직
- `rate-limiter-redis`: Redis 분산 제한
- `rate-limiter-spring`: Spring 통합
- `rate-limiter-spring-boot-starter`: 애플리케이션 진입점

## 경계

- 요청 속도 제한은 이 저장소의 책임이다.
- 인증 토큰 발급은 이 저장소의 책임이 아니다.
- 정책 엔진 평가와 감사 저장은 이 저장소의 책임이 아니다.

