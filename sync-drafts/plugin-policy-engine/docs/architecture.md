# Architecture

`plugin-policy-engine`는 정책을 조합하고 평가하는 플랫폼 구현 레포다.

## 설계 원칙

- 정책 평가는 플랫폼 책임이다.
- 서비스는 평가 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.
- Spring wiring은 adapter layer에 둔다.

## 구성 요소

- `plugin-policy-engine-core`: 정책 평가 핵심
- `plugin-policy-engine-spring`: Spring 통합
- `plugin-policy-engine-spring-boot-starter`: 애플리케이션 진입점

## 경계

- policy evaluation은 이 저장소의 책임이다.
- 정책 키 조회는 이 저장소의 책임이 아니다.
- 감사 저장은 이 저장소의 책임이 아니다.

