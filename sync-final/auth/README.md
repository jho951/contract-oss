# platform-security auth

`auth`는 `platform-security`의 인증 구현 레포다.
`auth` 자체가 1계층 OSS이고, `platform-security`는 그 위의 2계층이다.

## 책임

- 인증 처리
- principal 생성과 전달
- token 발급과 검증
- session 처리
- JWT 구현
- OAuth2 구현
- Spring 연동

## 권장 모듈

- `auth-core`
- `auth-jwt`
- `auth-session`
- `auth-hybrid`
- `auth-spring`
- `auth-spring-boot-starter`
- `auth-common-test`

## 모듈 설명

- `auth-core`: 핵심 인증 모델과 인터페이스
- `auth-jwt`: JWT 발급/검증
- `auth-session`: 세션 처리
- `auth-hybrid`: 조합 전략
- `auth-spring`: Spring 어댑터
- `auth-spring-boot-starter`: 소비 진입점
- `auth-common-test`: 테스트 지원

## SCM 메타데이터

- `github_org`: `jho951`
- `github_repo`: `auth`
- `url`, `connection`, `developerConnection`은 위 두 키를 조합한다.

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
