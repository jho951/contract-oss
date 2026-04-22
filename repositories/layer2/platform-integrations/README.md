# platform-integrations

## 기준

- GitHub: https://github.com/jho951/platform-integrations
- Version: `1.0.3`
- 계층: 2계층 optional integration platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)
- platform 표준: [../../../registry/layer2/standards/platform-integrations.md](../../../registry/layer2/standards/platform-integrations.md)

## 흡수 대상

- 별도 1계층 OSS를 흡수하지 않는다.
- 이미 존재하는 2계층 platform의 공개 계약을 선택적으로 연결한다.
- 외부 SaaS/API 연동 platform이 아니라 platform-to-platform bridge layer다.

## 책임

- `platform-security` security audit event를 `platform-governance` audit log로 연결
- `platform-resource` resource lifecycle event를 `platform-governance` audit log로 연결
- platform 본체 사이의 필수 의존성 증가 방지
- 소비자가 필요한 bridge만 명시적으로 추가할 수 있는 artifact 제공
- source platform event를 target platform 책임으로 전달하는 adapter 제공

## 현재 모듈

- `platform-security-governance-bridge`
- `platform-resource-governance-bridge`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/ownership.md`

## README / 문서 기준

- 공개 좌표는 실제 publish artifact와 일치해야 한다.
- 흡수 대상은 1계층 기준 버전과 충돌하지 않아야 한다.
- `무엇을 제공하나`는 `settings.gradle` include 목록과 일치해야 한다.
- 책임 경계에는 platform 조립 책임과 소비자 비즈니스 책임을 명확히 나눈다.
- `platform-integrations`는 optional bridge 성격을 README에서 명시한다.
- docs는 bridge 목적, 소비 의존성, publish 단위를 중심으로 둔다.
- 소비자별 비즈니스 정책이나 도메인 권한 판단을 platform 책임처럼 설명하지 않는다.

## 현재 version pin

- `securityVersion=2.1.0`
- `governanceVersion=2.0.2`
- `resourceVersion=2.0.2`
- `release_version=1.0.3`

## 실무 기준

- bridge는 source platform과 target platform을 모두 쓰는 소비자만 추가한다.
- `platform-security-governance-bridge`는 `SecurityAuditPublisher`를 governance 내부 `AuditLogRecorder` bean에 연결한다.
- `platform-resource-governance-bridge`는 `ResourceLifecyclePublisher`를 governance 내부 `AuditLogRecorder` bean에 연결한다.
- bridge는 보안 판단, resource 접근 판단, governance 정책 판단을 새로 만들지 않는다.
- bridge는 본체 platform을 대신 enable하지 않는다.
- bridge는 본체 platform 내부 구현 class를 직접 참조하지 않는다.
- bridge가 필요한 소비자는 본체 platform BOM/starter와 bridge artifact version을 모두 명시한다.
- formal docs에서는 repo 역할을 `optional integration platform`, 개별 publish module을 `bridge module` 또는 `bridge artifact`로 부른다.

## 배포 기준

- `securityVersion`, `governanceVersion`, `resourceVersion`은 exact version으로 pin한다.
- bridge artifact version은 `release_version`으로 관리한다.
- publish는 bridge module 단위로 수행할 수 있다.

## 현재 상태

- 구현 레포 `main`은 `security=2.1.0`, `governance=2.0.2`, `resource=2.0.2`, `release_version=1.0.3` 기준으로 정렬됐다.
- `platform-resource-governance-bridge:1.0.3`와 `platform-security-governance-bridge:1.0.3`가 모두 publish 완료 상태다.
- 서비스의 공식 governance 출력 SPI는 `AuditSink`다.
- bridge는 서비스 확장 포인트로 `AuditLogRecorder`를 노출하지 않고 governance 내부 `AuditLogRecorder` bean을 통해 기록한다.
