# Architecture

`audit-log`는 구조화된 감사 이벤트를 남긴다.

## 원칙

- 감사는 플랫폼 책임이다.
- 서비스는 감사 이벤트만 전달한다.
- 구현은 contract를 재정의하지 않는다.

## 구성

- `audit-log-api`
- `audit-log-core`
- `audit-log-autoconfigure`
- `audit-log-spring-boot-starter`
- `audit-log-common-test`

