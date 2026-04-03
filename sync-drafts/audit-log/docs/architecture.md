# Architecture

`audit-log`는 구조화된 감사 이벤트를 표준 필드로 남기는 플랫폼 구현 레포다.

## 설계 원칙

- 감사는 플랫폼 책임이다.
- 서비스는 감사 이벤트를 남기기만 한다.
- 구현은 contract를 재정의하지 않는다.
- Spring wiring은 adapter layer에 둔다.

## 구성 요소

- `audit-log-api`: 감사 이벤트 인터페이스
- `audit-log-core`: 핵심 이벤트 모델과 sink 로직
- `audit-log-spring-boot-autoconfigure`: Spring 자동 설정
- `audit-log-spring-boot-starter`: 애플리케이션 진입점

## 경계

- 감사 로그 기록은 이 저장소의 책임이다.
- 정책 엔진 평가는 이 저장소의 책임이 아니다.
- 인증 token 발급은 이 저장소의 책임이 아니다.

