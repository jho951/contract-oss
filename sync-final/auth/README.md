# platform-security auth

`auth`는 `platform-security`의 인증 구현 레포다.

## 책임

- 인증 처리
- principal 생성과 전달
- token 발급과 검증
- session 처리
- JWT 구현
- OAuth2 구현
- Spring 연동

## 기준

- 공통 계약과 경계 규칙은 [oss-contract](https://github.com/jho951/oss-contract)를 따른다.
- 실제 서비스 서버의 계약은 [service-contract](https://github.com/jho951/service-contract)를 따른다.

## 범위

- `auth-core`
- `auth-jwt`
- `auth-session`
- `auth-hybrid`
- `auth-spring`
- `auth-spring-boot-starter`
- `auth-common-test`

## 제외 범위

- 정책 저장
- 감사 로그 저장
- 파일 저장
- 서비스 비즈니스 로직

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)
5. [docs/oauth2-design.md](docs/oauth2-design.md)

