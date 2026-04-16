# platform-security

## 기준

- GitHub: https://github.com/jho951/platform-security
- Version: `1.0.4`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)
- platform 표준: [../../../registry/layer2/platform-security-standard.md](../../../registry/layer2/platform-security-standard.md)

## 흡수 대상

- `auth`
- `ip-guard`
- `rate-limiter`

## 책임

- boundary / client type / auth mode / evaluation result 모델
- authentication / IP guard / rate limit / downstream identity propagation 실행 체인
- Spring Boot 자동 구성
- 역할별 starter와 preset
- 내부 서비스 공통 보안 진입점

## 현재 모듈

- `platform-security-bom`
- `platform-security-policy`
- `platform-security-api`
- `platform-security-auth`
- `platform-security-ip`
- `platform-security-rate-limit`
- `platform-security-core`
- `platform-security-web`
- `platform-security-autoconfigure`
- `platform-security-starter`
- `platform-security-edge-starter`
- `platform-security-issuer-starter`
- `platform-security-resource-server-starter`
- `platform-security-internal-service-starter`
- `platform-security-test-support`
- `platform-security-sample-consumer`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/quickstart.md`
- `docs/architecture.md`
- `docs/configuration.md`
- `docs/extension-guide.md`
- `docs/modules.md`
- `docs/auth-server-integration.md`
- `docs/private-publish.md`
- `docs/security-model.md`
- `docs/troubleshooting.md`
