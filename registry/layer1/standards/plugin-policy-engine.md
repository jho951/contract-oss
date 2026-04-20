# plugin-policy-engine Standard

이 문서는 `plugin-policy-engine` 1계층 OSS의 표준 책임과 경계를 고정한다.

## 목적

- feature flag와 plugin policy 평가 primitive를 제공한다.
- targeting, eligibility, rollout, variant 선택을 순수 기능 모듈로 유지한다.
- 2계층 `platform-governance`가 feature flag config 호환 기준과 BOM 정렬 대상으로 소비할 수 있게 한다.

## 계층 원칙

- `plugin-policy-engine`은 1계층 OSS다.
- `plugin-policy-engine`은 feature flag / plugin policy evaluation primitive를 제공한다.
- `platform-governance`의 운영 정책 runtime 전체를 대신하지 않는다.
- governance audit, violation handling, service-role preset은 `platform-governance` 책임이다.

## 모듈 기준

- `plugin-policy-engine-api`
- `plugin-policy-engine-core`
- `plugin-policy-engine-config`

## 포함해야 할 것

- feature flag 평가 모델
- allow / deny targeting
- 속성 기반 eligibility
- deterministic rollout
- variant 선택
- `FlagStore` SPI
- 순수 Java 조립 API
- config binding primitive

## 포함하지 말아야 할 것

- governance audit pipeline
- governance violation handler
- 서비스별 flag taxonomy hardcoding
- Spring Boot service role preset
- platform bridge 구현

## 판정 기준

- feature flag나 plugin policy의 순수 평가 primitive면 `plugin-policy-engine` 책임이다.
- 운영 정책 실행 골격, audit 기록, 위반 대응까지 묶으면 `platform-governance` 책임이다.
