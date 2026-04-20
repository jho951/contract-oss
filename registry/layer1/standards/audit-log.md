# audit-log Standard

이 문서는 `audit-log` 1계층 OSS의 표준 책임과 경계를 고정한다.

## 목적

- 감사 이벤트, context, masking, sink 계약을 제공한다.
- 감사 기록 primitive를 순수 기능 모듈로 유지한다.
- 2계층 `platform-governance`가 audit pipeline과 운영 정책을 조립할 수 있게 한다.

## 계층 원칙

- `audit-log`는 1계층 OSS다.
- `audit-log`는 event schema와 sink primitive를 제공한다.
- 정책 평가, 위반 처리, service-role preset, identity audit convenience API는 `platform-governance` 책임이다.
- 소비자별 audit taxonomy와 도메인 사건 의미는 1계층 책임이 아니다.

## 모듈 기준

- `audit-log-api`
- `audit-log-core`

## 포함해야 할 것

- audit event 모델
- audit context 모델
- masking SPI
- sink 계약
- 기본 logger와 범용 sink 구현
- recorder primitive

## 포함하지 말아야 할 것

- governance 정책 평가 runtime
- identity/resource/security 전용 audit taxonomy hardcoding
- 서비스별 audit key 규칙
- violation handler orchestration
- platform bridge 구현

## 판정 기준

- 감사 이벤트를 표현하고 sink로 전달하는 primitive면 `audit-log` 책임이다.
- 어떤 운영 사건을 어떤 taxonomy로 기록하고 정책 위반과 연결할지 정하면 `platform-governance` 책임이다.
