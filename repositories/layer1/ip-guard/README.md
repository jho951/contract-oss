# ip-guard

## 기준

- GitHub: https://github.com/jho951/ip-guard
- Version: `3.0.0`
- 계층: 1계층 OSS
- registry 기준: [../../../registry/layer1/README.md](../../../registry/layer1/README.md)

## 책임

- IP 접근 제어 계약
- 입력 / 출력 모델
- SPI
- IP / rule 파싱과 매칭
- 결정 엔진
- IPv4/IPv6 single, CIDR, range, IPv4 wildcard 규칙 문법

## 현재 모듈

- `ip-guard-core`
- `ip-guard-spi`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/rule-syntax.md`
- `docs/extension-guide.md`
- `docs/test-and-ci.md`
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

- `docs/test-and-ci.md`를 `docs/testing-and-ci.md`로 변경
- `License`를 `LICENSE`로 통일
