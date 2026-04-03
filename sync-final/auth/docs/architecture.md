# Architecture

`auth`는 요청 진입 보안에서 인증을 담당한다.

## 원칙

- 인증은 플랫폼 책임이다.
- 서비스는 인증 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.
- Spring 연동은 adapter layer에 둔다.

## 구성

- `auth-core`
- `auth-jwt`
- `auth-session`
- `auth-hybrid`
- `auth-spring`
- `auth-spring-boot-starter`

