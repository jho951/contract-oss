# platform-governance Standard

이 문서는 `platform-governance`가 L5 목표 구조에서 어떤 책임을 가져야 하는지 고정한다.

## 적용 범위

- 이 문서는 현재 조직이 운영하는 governance 2계층 line으로서의 `platform-governance` 기준을 정의한다.
- 이것이 2계층 governance platform의 유일한 형태라는 뜻은 아니다.
- 다른 팀이나 프로젝트도 같은 1계층 OSS (`audit-log`, `policy-config`, `plugin-policy-engine`)를 사용해 다른 governance 2계층 line을 만들 수 있다.
- 다만 서비스나 다른 platform은 raw OSS 대신 자신이 선택한 governance platform line의 contract를 소비해야 한다.

## 역할

- 감사와 정책과 운영 통제 플랫폼
- audit, policy config, policy engine, violation handling의 표준 계층

## 목적

- 서비스마다 audit 포맷과 policy 호출 방식을 따로 만들지 않게 한다.
- 운영 기준, 감사 기준, 정책 기준을 현재 조직 표준 방식으로 제공한다.
- `platform-security`, `platform-resource`, `platform-integrations`가 같은 정책과 감사 기준을 보게 한다.

## 소유해야 할 것

- audit event 표준 모델
- audit sink 표준화
- policy config loading
- plugin policy engine 실행
- 운영 정책 평가 결과 표준화
- violation handler
- 운영 기본값과 fail-fast 기준

## 1계층 조립 기준

- `audit-log`
- `policy-config`
- `plugin-policy-engine`

## 포함해야 할 것

- platform-owned audit contract
- platform-owned policy contract
- 정책 조회와 평가 엔진
- audit convenience API
- typed properties
- 운영 fail-fast

## 현재 main 기준 public SPI

- `GovernanceAuditSink`
- `GovernanceAuditRecorder`
- `PolicyConfigSource`
- `GovernanceDecisionEngine`
- `ViolationHandler`

이 다섯 축은 현재 `platform-governance` line에서 서비스와 다른 platform이 보는 public governance surface다.

## 포함하지 말아야 할 것

- 인증 필터 체인
- JWT 발급과 세션 집행
- 파일 저장과 삭제 구현
- 메일 발송과 webhook 호출
- 서비스별 도메인 승인 로직

## 확장 규칙

- `platform-governance`는 정책과 감사 기준의 owner다.
- 요청을 실제로 차단하거나 인증 흐름에서 집행하는 owner는 `platform-security`다.
- domain fact 판단은 소비자 서비스 책임이다.
- `plugin-policy-engine` 전체 runtime을 다시 platform 바깥으로 흘려보내지 않는다.

## local layer1 검증 기준

- `./gradlew check -PuseLocalLayer1=true` 경로를 유지한다.
- local source 검증은 `../../oss/audit-log`, `../../oss/policy-config`, `../../oss/plugin-policy-engine` includeBuild를 기준으로 본다.
- dependency locking 완화는 local source 검증 모드에서만 허용하고, 일반 publish/check 경로에는 적용하지 않는다.

## 검증 기준

- `verifyPublishedSurface`는 audit, policy, violation handling public SPI가 publish surface에 포함되는지 확인해야 한다.
- `verifyStarterContract`는 governance starter 하나로 운영 기본값과 audit/policy wiring이 붙는지 확인해야 한다.
- `verifyConsumerConformance`는 sample consumer가 raw OSS contract를 직접 조립하지 않아도 되는지 확인해야 한다.
- `verifyStage5Contract`는 public surface에 1계층 audit/policy 타입이 새지 않았는지 확인해야 한다.

## 운영 기준

- production profile 기본값은 `["prod", "production"]`를 사용한다.
- audit sink, service identity, policy operational status는 fail-fast 대상이다.
