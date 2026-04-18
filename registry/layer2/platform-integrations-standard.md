# platform-integrations Standard

이 문서는 `platform-integrations` 2계층 platform의 표준 구조와 경계를 고정한다.

## 목적

- `platform-security`, `platform-resource`, `platform-governance`처럼 이미 독립적인 platform 사이의 선택 연결을 관리한다.
- 본체 platform이 서로를 필수 의존성으로 끌어안지 않도록 bridge를 별도 artifact로 분리한다.
- 소비자가 필요한 연결만 명시적으로 추가할 수 있게 한다.

## 계층 원칙

- `platform-integrations`는 2계층 optional integration platform이다.
- formal docs에서는 repository 역할을 `optional integration platform`으로 부른다.
- individual published module은 `bridge module` 또는 `bridge artifact`로 부른다.
- bridge는 source platform의 공개 event/publisher 계약과 target platform의 공개 recorder 계약만 사용한다.
- bridge는 소비자 비즈니스 로직, 도메인 권한 판단, 소비자별 policy key를 포함하지 않는다.
- bridge는 본체 platform의 release 단위와 독립적으로 release할 수 있다.
- bridge는 두 platform을 모두 쓰는 소비자가 `implementation`으로 명시할 때만 활성화된다.

## 현재 모듈 기준

- `platform-security-governance-bridge`
- `platform-resource-governance-bridge`

## bridge 책임

| Bridge | Source | Target | 책임 |
| --- | --- | --- | --- |
| `platform-security-governance-bridge` | `platform-security` | `platform-governance` | security audit event를 governance audit entry로 기록 |
| `platform-resource-governance-bridge` | `platform-resource` | `platform-governance` | resource store/delete lifecycle event를 governance audit entry로 기록 |

## 소비 기준

소비자는 아래 조건을 모두 만족할 때만 bridge를 추가한다.

- source platform을 이미 사용한다.
- target platform을 이미 사용한다.
- event를 target platform audit으로 남겨야 하는 운영 요구가 있다.
- 기본 bridge mapping으로 충분하거나, 별도 publisher/recorder override point가 있다.

## 포함하지 말아야 할 것

- `platform-security` 내부 filter나 policy 구현 직접 참조
- `platform-resource` 내부 workflow 구현 직접 참조
- `platform-governance` 내부 audit 구현 직접 참조
- 소비자별 audit taxonomy 하드코딩
- 소비자별 권한 판단
- bridge가 본체 platform을 대신 enable하는 자동 조립

## 정합성 기준

- `platform-security-governance-bridge`는 `SecurityAuditPublisher`와 `AuditLogRecorder` 계약으로만 연결한다.
- `platform-resource-governance-bridge`는 `ResourceLifecyclePublisher`와 `AuditLogRecorder` 계약으로만 연결한다.
- `platform-resource-governance-bridge` source, tests, build script, publish configuration, artifact version, release tag는 `platform-integrations`가 소유한다.
- `platform-resource`는 `ResourceLifecycleEvent`, `ResourceLifecyclePublisher`, lifecycle publisher composition, lifecycle mode fail-fast rule만 소유한다.
- 연결 대상 platform version은 `gradle.properties`에 exact version으로 pin한다.
- bridge release version은 `platform-integrations`의 `release_version`으로 관리한다.
- publish는 bridge module 단위로 수행할 수 있다.

## 실무 판단 기준

- "이 기능이 없어도 source platform이 정상 동작해야 한다"면 bridge가 맞다.
- "두 platform을 모두 쓰는 소비자에게만 필요한 연결"이면 bridge가 맞다.
- "source platform의 핵심 실행 흐름 자체"라면 bridge가 아니라 source platform 본체 책임이다.
- "소비자 도메인에 따라 의미가 달라지는 audit 분류"라면 bridge가 아니라 소비자 override 책임이다.
