# platform-governance Standard

이 문서는 `platform-governance` 2계층 platform의 표준 구조와 경계를 고정한다.

## 목적

- `audit-log`, `policy-config` 1계층 OSS와 `plugin-policy-engine-config` 호환 기준을 조립하는 표준 2계층을 정의한다.
- 운영 정책, 감사 기록, 정책 평가와 위반 대응의 공통 runtime을 제공한다.
- security/resource 같은 다른 platform이 직접 governance 구현을 알지 않아도 되는 공개 recorder/API 경계를 제공한다.

## 계층 원칙

- `platform-governance`는 서비스가 직접 소비하는 runtime platform이다.
- governance는 보안의 하위 계층이 아니라 security와 나란히 붙는 운영 통제 platform이다.
- `policy-config`, audit pipeline, platform `GovernancePolicyPlugin` chain의 owner는 `platform-governance`다.
- `plugin-policy-engine` 전체 runtime은 흡수하지 않고 feature flag/config 호환 기준과 BOM 정렬 대상으로만 둔다.
- governance 판단은 운영 정책과 감사/위반 처리의 표준화에 한정한다.
- 업무 승인, 게시글 권한, workspace membership 같은 도메인 사실 판단은 소비자 서비스 책임이다.
- security/resource event를 governance audit으로 연결하는 bridge는 `platform-integrations`에서 제공한다.

## 1계층 조립 기준

- `audit-log`: 구조화 audit event, sink, masking, recorder primitive
- `policy-config`: 운영 정책 설정 source, resolution, operational status
- `plugin-policy-engine-config`: feature flag/config 호환 기준과 BOM 정렬 대상

## 포함해야 할 것

- 구조화 감사 API와 taxonomy
- identity audit recorder 같은 역할별 audit convenience API
- 정책 설정 조회와 feature flag config 호환 기준
- platform `GovernancePolicyPlugin` chain 조립
- 정책 변경 기록
- 위반 대응 handler 실행
- service role preset 기반 운영 기본값
- `AuditSink`, `AuditLogRecorder` 같은 integration API
- 운영 fail-fast 정책

## 포함하지 말아야 할 것

- security filter, authentication, gateway header 인증 조립
- resource 저장, 삭제, catalog 구현
- 소비자별 audit taxonomy 하드코딩
- 소비자별 policy key 하드코딩
- 도메인 권한 판단
- 특정 서비스 DB 상태 확인
- security/resource event bridge 구현

## 확장 규칙

- 감사 출력 대상은 `AuditSink`를 공식 SPI로 본다.
- `AuditLogRecorder`는 governance event를 audit pipeline으로 넘기는 adapter 계약으로 본다.
- 정책 평가는 platform `GovernancePolicyPlugin` 또는 `GovernanceDecisionEngine`으로 확장한다.
- audit 기록과 violation handling 골격은 platform이 소유한다.
- feature flag config 설정 prefix는 `platform.governance.feature-flags.*`를 사용한다.
- 기존 `platform.governance.plugin-policy-engine.*`는 deprecated alias로만 유지한다.

## 운영 기준

- 운영에서는 audit sink/context/service identity, `PolicyConfigSource.operationalStatus()`, fatal handler 정책을 fail-fast 대상으로 본다.
- `platform-governance-core`는 Spring/audit/violation wrapper 없는 pure Java reference engine으로 유지한다.
- bridge가 필요한 소비자는 `platform-integrations`의 bridge artifact를 명시적으로 추가한다.
