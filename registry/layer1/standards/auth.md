# auth Standard

이 문서는 `auth` 1계층 OSS의 표준 책임과 경계를 고정한다.

## 역할

- 인증 capability 계약과 인증 수단별 primitive를 제공하는 1계층 OSS
- principal, token, session, credential, verifier 모델을 제공하는 순수 기능 계층

## 목적

- 인증 수단 자체의 계약과 검증 primitive를 1계층에 둔다.
- 현재 조직 표준 security line인 `platform-security`가 이 primitive를 조립할 수 있게 한다.
- 같은 primitive를 바탕으로 다른 security 2계층 line도 만들 수 있게 한다.

## 계층 원칙

- `auth`는 1계층 OSS다.
- `auth`는 Spring Boot starter나 서비스별 `SecurityConfig`를 소유하지 않는다.
- 요청 보안 체인 조립, gateway trusted header 처리, rate limit과 IP guard 결합은 2계층 security platform 책임이다.
- 회원가입, 로그인 화면, 사용자 DB 상태 판단, 서비스별 권한 정책은 서비스 책임이다.

## 모듈 기준

- `auth-core`
- `auth-jwt`
- `auth-session`
- `auth-hybrid`
- `auth-apikey`
- `auth-hmac`
- `auth-oidc`
- `auth-service-account`

## 포함해야 할 것

- principal, credential, token, session 모델
- JWT 검증 primitive
- session 검증 primitive
- JWT/session hybrid 인증 primitive
- API key, HMAC, OIDC, service account 인증 primitive
- 인증 결과와 실패 모델
- 2계층 platform이 조립할 수 있는 SPI

## 포함하지 말아야 할 것

- Spring Security filter chain 조립
- gateway trusted header 처리
- 서비스별 `JwtDecoder` bean 조립
- 회원가입, 로그인 화면, 사용자 관리 업무
- 특정 서비스 URL, Redis key, DB schema 규칙
- 도메인 권한 판단

## 판정 기준

- 인증 수단의 순수 검증과 모델이면 `auth` 책임이다.
- 요청 진입 보안 파이프라인, gateway header, rate limit, IP guard와 함께 조립되면 2계층 security platform 책임이다.
