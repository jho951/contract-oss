# OAuth2 Design

이 문서는 `auth` 저장소의 OAuth2 책임을 정리한다.

## 역할

- OAuth2 principal resolution
- OAuth2 login 연동
- 토큰 발급 흐름 연계

## 경계

- OAuth2는 인증 구현의 한 방식이다.
- OAuth2는 정책 엔진이 아니다.
- OAuth2는 감사 저장소가 아니다.

## 연동 원칙

- Spring 연동은 adapter layer에 둔다.
- 핵심 인증 모델은 Spring에 종속되지 않는다.
- 계약은 `oss-contract`와 `service-contract`를 우선한다.

