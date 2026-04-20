# platform-governance

## 기준

- GitHub: https://github.com/jho951/platform-governance
- Version: `2.0.1`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)
- platform 표준: [../../../registry/layer2/platform-governance-standard.md](../../../registry/layer2/platform-governance-standard.md)

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
- `release_version=2.0.1`
- `platformReleaseVersion=2.0.1`

## 현재 모듈

- `platform-governance-bom`
- `platform-governance-api`
- `platform-governance-audit`
- `platform-governance-config`
- `platform-governance-core`
- `platform-governance-engine`
- `platform-governance-spring`
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

## 실무 기준

- 소비자는 `platform-governance-starter`와 `platform.governance.service-role-preset`을 기본 진입점으로 사용한다.
- `identity-service`, `policy-decision-service`, `resource-service`, `observability-service` preset은 이름이 아니라 governance 주 역할이다.
- identity 역할 소비자는 범용 audit entry를 직접 만들기보다 `IdentityAuditRecorder`를 우선 사용한다.
- production 감사 출력 대상은 `AuditSink`를 공식 SPI로 보고, `AuditLogRecorder`는 governance event를 audit pipeline으로 넘기는 adapter로 본다.
- 정책 평가는 platform `GovernancePolicyPlugin` 또는 `GovernanceDecisionEngine`으로 확장하고, audit 기록과 violation handling 골격은 platform에 둔다.
- `platform-governance-core`는 Spring/audit/violation wrapper 없는 pure Java reference engine으로 유지한다.
- feature flag config 설정 prefix는 `platform.governance.feature-flags.*`를 사용하고, 기존 `platform.governance.plugin-policy-engine.*`는 deprecated alias로만 유지한다.
- 운영에서는 audit sink/context/service identity, `PolicyConfigSource.operationalStatus()`, fatal handler 정책을 fail-fast 대상으로 본다.
- security/resource event를 governance audit으로 연결하는 구현은 `platform-integrations`의 bridge가 소유한다.
- 업무 승인, 게시글 권한, workspace membership 같은 도메인 사실 판단은 소비자 서비스가 소유한다.
- `plugin-policy-engine` 전체 runtime을 흡수하거나 adapter로 재포장하지 않고, feature flag/config 호환 기준과 BOM 정렬 대상으로만 둔다.

## 정리 후보

- 원격 `platform-governance`는 `auditLogVersion=2.0.0`, `policyConfigVersion=2.0.0`을 pin하지만, 현재 각 1계층 원격 `main`의 `release_version`은 `audit-log=2.0.1`, `policy-config=1.0.1`이다. 의도된 published pin인지 확인이 필요하다.
