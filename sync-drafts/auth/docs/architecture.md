# Architecture

`auth`는 요청 진입 보안에서 인증 책임을 담당하는 구현 레포다.

## 설계 원칙

- 인증은 플랫폼 책임이다.
- 서비스는 인증 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.
- Spring wiring은 구현 레이어에 둔다.

## 구성 요소

- `auth-core`: 인증 도메인과 공통 인터페이스
- `auth-jwt`: JWT 기반 토큰 처리
- `auth-session`: 세션 기반 처리
- `auth-hybrid`: JWT + session 조합
- `auth-spring`: Spring 통합
- `auth-spring-boot-starter`: 애플리케이션 진입점

## 경계

- principal 생성은 이 저장소의 책임이다.
- token 검증은 이 저장소의 책임이다.
- policy decision은 이 저장소의 책임이 아니다.
- audit logging은 이 저장소의 책임이 아니다.

