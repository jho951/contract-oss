# Architecture

`rate-limiter`는 요청량을 제어한다.

## 원칙

- rate limit은 플랫폼 책임이다.
- 서비스는 제한 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.

## 구성

- `rate-limiter-core`
- `rate-limiter-redis`
- `rate-limiter-spring`
- `rate-limiter-spring-boot-starter`

