# Architecture

`ip-guard`는 요청 진입 시점의 IP 제어를 담당한다.

## 원칙

- IP 판단은 플랫폼 책임이다.
- 서비스는 판단 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.

## 구성

- `ip-guard-core`
- `ip-guard-spring`
- `ip-guard-spring-boot-starter`

