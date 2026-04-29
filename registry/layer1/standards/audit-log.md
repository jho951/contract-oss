# audit-log Standard

이 문서는 `audit-log` 1계층 OSS의 표준 책임과 경계를 고정한다.

## 역할

- 감사 이벤트와 sink primitive를 제공하는 1계층 OSS
- audit event, context, masking, recorder를 제공하는 순수 기능 계층

## 목적

- 감사 이벤트, context, masking, sink 계약을 1계층에 둔다.
- 현재 조직 표준 governance line인 `platform-governance`가 audit runtime을 조립할 수 있게 한다.
- 같은 primitive를 바탕으로 다른 governance 2계층 line도 만들 수 있게 한다.

## 계층 원칙

- `audit-log`는 1계층 OSS다.
- `audit-log`는 event schema와 sink primitive를 제공하고 운영 taxonomy나 platform orchestration은 소유하지 않는다.
- identity, resource, security 같은 audit taxonomy 표준화는 2계층 governance platform 책임이다.
- 서비스별 audit 사건 의미와 domain-specific key 규칙은 소비자 또는 2계층 platform 책임이다.

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
- identity, resource, security 전용 audit taxonomy hardcoding
- 서비스별 audit key 규칙
- violation handler orchestration
- platform bridge 구현

## 판정 기준

- 감사 이벤트를 기록하기 위한 순수 모델과 sink primitive면 `audit-log` 책임이다.
- audit taxonomy를 정하고 정책 평가나 위반 대응과 엮어 운영 기준으로 만드는 것은 2계층 governance platform 책임이다.
