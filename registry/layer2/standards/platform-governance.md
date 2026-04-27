# platform-governance Standard

이 문서는 `platform-governance`가 L5 목표 구조에서 어떤 책임을 가져야 하는지 고정한다.

## 역할

- 감사와 정책과 운영 통제 플랫폼
- audit, policy config, policy engine, violation handling의 표준 계층

## 목적

- 서비스마다 audit 포맷과 policy 호출 방식을 따로 만들지 않게 한다.
- 운영 기준, 감사 기준, 정책 기준을 한 곳에서 고정한다.
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

## 운영 기준

- production profile 기본값은 `["prod", "production"]`를 사용한다.
- audit sink, service identity, policy operational status는 fail-fast 대상이다.
