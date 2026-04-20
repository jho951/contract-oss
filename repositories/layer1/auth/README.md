# auth

## 기준

- GitHub: https://github.com/jho951/auth
- Version: `3.0.1`
- 계층: 1계층 OSS
- registry 기준: [../../../registry/layer1/README.md](../../../registry/layer1/README.md)
- OSS 표준: [../../../registry/layer1/standards/auth.md](../../../registry/layer1/standards/auth.md)

## README 기준

- 공개 좌표는 실제 publish artifact와 일치해야 한다.
- `무엇을 제공하나`는 `settings.gradle` include 목록과 일치해야 한다.
- 책임 경계에는 1계층 책임과 2계층 platform 책임을 명확히 나눈다.
- SOT 내부 동기화 문서를 레포 README에 안내하지 않는다.

## 책임

- 인증 capability 계약
- principal / token / session 모델
- JWT / session / hybrid / API key / HMAC / OIDC / service account 인증 수단
- 범용 인증 SPI

## 현재 모듈

- `auth-core`
- `auth-jwt`
- `auth-session`
- `auth-hybrid`
- `auth-apikey`
- `auth-hmac`
- `auth-oidc`
- `auth-service-account`

## 현재 문서

- `README.md`
- `docs/readme.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/implementation-guide.md`
- `docs/test-and-ci.md`
- `docs/troubleshooting.md`

## 문서 기준

- 파일명은 소문자 `kebab-case`를 사용한다.
- 테스트/CI 문서는 `docs/test-and-ci.md`로 통일한다.
- 대문자 docs 파일명은 새 기준으로 추가하지 않는다.
- `docs/implementation-guide.md`는 레포 책임에 필요한 경우에만 둔다.
- 레포별 특화 문서는 OSS 표준의 책임 범위 안에서만 둔다.

## 현재 운영 파일

- `.github/ISSUE_TEMPLATE/*`
- `.github/pull_request_template.md`
- `.github/workflows/build.yml`
- `.github/workflows/publish.yml`
- `CONTRIBUTING.md`
- `License`
- `SECURITY.md`
- `SUPPORT.md`

## 정리 후보

- `License`를 `LICENSE`로 통일
