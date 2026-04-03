# Modules

이 저장소의 모듈은 rate limit 책임을 분리해서 담는다.

## 모듈 역할

- `rate-limiter-core`: 핵심 제한 규칙
- `rate-limiter-redis`: Redis 기반 분산 제한
- `rate-limiter-spring`: Spring 어댑터
- `rate-limiter-spring-boot-starter`: 자동 설정 진입점

## 모듈 원칙

- 핵심 규칙은 core에 둔다.
- 분산 저장소 종속성은 별도 모듈로 격리한다.
- Spring 종속성은 adapter와 starter로 격리한다.

