# platform-governance

## 기준

- GitHub: https://github.com/jho951/platform-governance
- Version: `2.0.0`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)

## 흡수 대상

- `audit-log`
- `policy-config`
- `plugin-policy-engine`

## 책임

- 구조화 감사
- identity audit 표준 API와 taxonomy
- 정책 설정 조회
- 정책 평가 엔진 조립
- 정책 변경 기록
- 위반 대응 handler 실행
- 역할 preset 기반 운영 기본값 보강
- 1계층 governance OSS 배포본 소비 기준 고정
- governance integration API 제공

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
- 정책 평가는 `GovernancePolicyPlugin` 또는 `GovernanceDecisionEngine`으로 확장하고, audit 기록과 violation handling 골격은 platform에 둔다.
- 운영에서는 audit sink/context/service identity, policy config, fatal handler 정책을 fail-fast 대상으로 본다.
