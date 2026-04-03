# Architecture

`ip-guard`는 요청 진입 시점의 IP 제어를 담당하는 구현 레포다.

## 설계 원칙

- IP 판단은 플랫폼 책임이다.
- 서비스는 판단 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.
- Spring wiring은 adapter layer에 둔다.

## 구성 요소

- `ip-guard-core`: IP 판별 핵심 로직
- `ip-guard-spring`: Spring 통합
- `ip-guard-spring-boot-starter`: 애플리케이션 진입점

## 경계

- IP 허용/차단은 이 저장소의 책임이다.
- 인증 token 발급은 이 저장소의 책임이 아니다.
- 정책 엔진 평가와 감사 저장은 이 저장소의 책임이 아니다.

