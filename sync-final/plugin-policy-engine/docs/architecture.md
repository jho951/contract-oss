# Architecture

`plugin-policy-engine`는 정책을 조합하고 평가한다.

## 원칙

- 정책 평가는 플랫폼 책임이다.
- 서비스는 평가 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.

## 구성

- `plugin-policy-engine-core`
- `plugin-policy-engine-spring`
- `plugin-policy-engine-spring-boot-starter`
- `plugin-policy-engine-common-test`

