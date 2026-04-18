# platform-integrations

## 기준

- GitHub: https://github.com/jho951/platform-integrations
- Version: `1.0.0`
- 계층: 2계층 optional integration platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)
- platform 표준: [../../../registry/layer2/platform-integrations-standard.md](../../../registry/layer2/platform-integrations-standard.md)

## 흡수 대상

- 별도 1계층 OSS를 흡수하지 않는다.
- 이미 존재하는 2계층 platform의 공개 계약을 선택적으로 연결한다.

## 책임

- `platform-security` security audit event를 `platform-governance` audit log로 연결
- `platform-resource` resource lifecycle event를 `platform-governance` audit log로 연결
- platform 본체 사이의 필수 의존성 증가 방지
- 소비자가 필요한 bridge만 명시적으로 추가할 수 있는 artifact 제공

## 현재 모듈

- `platform-security-governance-bridge`
- `platform-resource-governance-bridge`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/ownership.md`

## 실무 기준

- bridge는 source platform과 target platform을 모두 쓰는 소비자만 추가한다.
- `platform-security-governance-bridge`는 `SecurityAuditPublisher`와 `AuditLogRecorder` 공개 계약만 연결한다.
- `platform-resource-governance-bridge`는 `ResourceLifecyclePublisher`와 `AuditLogRecorder` 공개 계약만 연결한다.
- bridge는 보안 판단, resource 접근 판단, governance 정책 판단을 새로 만들지 않는다.
- bridge가 필요한 소비자는 본체 platform BOM/starter와 bridge artifact version을 모두 명시한다.
- formal docs에서는 repo 역할을 `optional integration platform`, 개별 publish module을 `bridge module` 또는 `bridge artifact`로 부른다.

## 배포 기준

- `securityVersion`, `governanceVersion`, `resourceVersion`은 exact version으로 pin한다.
- bridge artifact version은 `release_version`으로 관리한다.
- publish는 bridge module 단위로 수행할 수 있다.
