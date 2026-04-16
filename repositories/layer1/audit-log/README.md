# audit-log

## 기준

- GitHub: https://github.com/jho951/audit-log
- Version: `2.0.0`
- 계층: 1계층 OSS
- registry 기준: [../../../registry/layer1/README.md](../../../registry/layer1/README.md)

## 책임

- 감사 이벤트 표준 모델
- 감사 logger / sink 계약
- context / masking SPI
- 기본 logger와 범용 sink 구현

## 현재 모듈

- `audit-log-api`
- `audit-log-core`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/ARCHITECTURE.md`
- `docs/CONFIGURATION.md`
- `docs/RUNBOOK.md`
- `docs/TROUBLESHOOTING.md`
- `docs/USAGE.md`
- `docs/implementation-guide.md`

## 현재 운영 파일

- `.github/ISSUE_TEMPLATE/*`
- `.github/Pull_request_template.md`
- `.github/workflows/build.yml`
- `.github/workflows/publish.yml`
- `CONTRIBUTING.md`
- `LICENSE`
- `SECURITY.md`
- `SUPPORT.md`

## 정리 후보

- `build/` 디렉터리 제거
- `.github/Pull_request_template.md`를 `.github/pull_request_template.md`로 변경
- docs 파일명을 소문자 kebab-case 기준으로 정리
- `docs/architecture.md`, `docs/modules.md`, `docs/extension-guide.md`, `docs/testing-and-ci.md`, `docs/troubleshooting.md` 기준 충족 여부 확인
