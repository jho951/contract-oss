# platform-governance

## 기준

- GitHub: https://github.com/jho951/platform-governance
- Version: `3.0.1`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)
- platform 표준: [../../../registry/layer2/standards/platform-governance.md](../../../registry/layer2/standards/platform-governance.md)

## 흡수 대상

- `audit-log`
- `policy-config`
- `plugin-policy-engine-config` 호환 기준

## 책임

- 구조화 감사
- identity audit 표준 API와 taxonomy
- 정책 설정 조회
- platform `GovernancePolicyPlugin` chain 조립
- 정책 변경 기록
- 위반 대응 handler 실행
- feature flag config 호환 기준 제공
- 역할 preset 기반 운영 기본값 보강
- 1계층 governance OSS 배포본 소비 기준 고정
- governance integration API 제공
- `policy-config`, audit pipeline, feature flag config 호환 기준 owner

## 현재 version pin

- `auditLogVersion=2.0.0`
- `policyConfigVersion=2.0.0`
- `pluginPolicyEngineVersion=2.0.1`
- `release_version=3.0.1`
- `platformReleaseVersion=3.0.1`

## 현재 모듈

- `platform-governance-bom`
- `platform-governance-api`
- `platform-governance-adapter-auditlog`
- `platform-governance-adapter-policyconfig`
- `platform-governance-core`
- `platform-governance-engine`
- `platform-governance-autoconfigure`
- `platform-governance-starter`
- `platform-governance-common-test`
- `platform-governance-samples`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/configuration.md`
- `docs/dependency-basis.md`
- `docs/examples/auth-server.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/governance-model.md`
- `docs/private-publish.md`
- `docs/troubleshooting.md`
- `docs/quality-gates.md`

## README / 문서 기준

- 공개 좌표는 실제 publish artifact와 일치해야 한다.
- 흡수 대상은 1계층 기준 버전과 충돌하지 않아야 한다.
- `무엇을 제공하나`는 `settings.gradle` include 목록과 일치해야 한다.
- 책임 경계에는 platform 조립 책임과 소비자 비즈니스 책임을 명확히 나눈다.
- docs는 platform 소비와 확장에 필요한 문서만 둔다.
- 소비자별 비즈니스 정책이나 도메인 권한 판단을 platform 책임처럼 설명하지 않는다.

## 실무 기준

- 소비자는 `platform-governance-starter`와 `platform.governance.service-role-preset`을 기본 진입점으로 사용한다.
- compile classpath stage-5 기준에서 `platform-governance-starter`는 `platform-governance-core`, `platform-governance-engine`, adapter 구현을 직접 새지 않는다.
- `identity-service`, `policy-decision-service`, `resource-service`, `observability-service` preset은 이름이 아니라 governance 주 역할이다.
- identity 역할 소비자는 범용 audit entry를 직접 만들기보다 `IdentityAuditRecorder`를 우선 사용한다.
- production 감사 출력 대상은 `AuditSink`를 공식 SPI로 보고, `AuditLogRecorder`는 governance event를 audit pipeline으로 넘기는 adapter로 본다.
- 서비스가 `AuditSink`, `AuditLogger`, `AuditEvent`를 코드에서 직접 import하면 `io.github.jho951:audit-log-api`를 명시적으로 추가한다.
- 정책 평가는 platform `GovernancePolicyPlugin` 또는 `GovernanceDecisionEngine`으로 확장하고, audit 기록과 violation handling 골격은 platform에 둔다.
- `platform-governance-core`는 Spring/audit/violation wrapper 없는 pure Java reference engine으로 유지한다.
- feature flag config 설정 prefix는 `platform.governance.feature-flags.*`를 사용하고, 기존 `platform.governance.plugin-policy-engine.*`는 deprecated alias로만 유지한다.
- 운영에서는 audit sink/context/service identity, `PolicyConfigSource.operationalStatus()`, fatal handler 정책을 fail-fast 대상으로 본다.
- security/resource event를 governance audit으로 연결하는 구현은 `platform-integrations`의 bridge가 소유한다.
- 서비스는 공식 SPI인 `AuditSink`, `PolicyConfigSource`, `GovernanceDecisionEngine`을 우선 사용하고, `AuditLogRecorder` 같은 adapter bean을 직접 extension point처럼 다루지 않는다.
- 업무 승인, 게시글 권한, workspace membership 같은 도메인 사실 판단은 소비자 서비스가 소유한다.
- `plugin-policy-engine` 전체 runtime을 흡수하거나 adapter로 재포장하지 않고, feature flag/config 호환 기준과 BOM 정렬 대상으로만 둔다.

## 의존성 pin 기준

- `platform-governance 3.0.1`의 현재 published 기준 pin은 `auditLogVersion=2.0.0`, `policyConfigVersion=2.0.0`, `pluginPolicyEngineVersion=2.0.1`이다.
- 따라서 `oss-contract`는 1계층 최신 `main` 버전이 아니라, 2계층 `platform-governance`가 실제로 pin한 published 좌표를 SoT로 본다.

## 현재 상태

- 현재 릴리스 기준은 `3.0.1`이다.
- 서비스의 공식 감사 출력 SPI는 `AuditSink`다.
- `platform-integrations` bridge는 서비스가 등록한 `AuditSink`에 직접 쓰지 않고 governance 내부 `AuditLogRecorder` bean을 통해 기록한다.
- 따라서 서비스는 custom `AuditLogRecorder`가 아니라 계속 `AuditSink`를 등록한다.
- `platform-governance-starter`만으로는 `AuditSink` 타입이 compile surface에 자동 노출되지 않으므로, SPI를 직접 구현하는 서비스는 `audit-log-api`를 별도 의존성으로 가진다.
- 구현 레포 `main` push와 `v3.0.1` publish까지 완료됐다.
- cross-repo release/publish 오류와 복구 이력은 [../../../troubleshooting.md](../../../troubleshooting.md)를 canonical record로 본다.
