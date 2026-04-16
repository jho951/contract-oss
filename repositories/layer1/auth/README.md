# auth

## 기준

- GitHub: https://github.com/jho951/auth
- Version: `3.0.1`
- 계층: 1계층 OSS
- registry 기준: [../../../registry/layer1/README.md](../../../registry/layer1/README.md)

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
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/implementation-guide.md`
- `docs/testing-and-ci.md`
- `docs/troubleshooting.md`

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
