# Architecture

`policy-config`는 다양한 설정 소스에서 정책 값을 읽어온다.

## 원칙

- 정책 설정 조회는 플랫폼 책임이다.
- 서비스는 조회 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.

## 구성

- `policy-config-core`
- `policy-config-spring`
- `policy-config-spring-boot-starter`
- `policy-config-common-test`

