# policy-config Standard

이 문서는 `policy-config` 1계층 OSS의 표준 책임과 경계를 고정한다.

## 역할

- 정책 설정 조회와 타입 안전한 key primitive를 제공하는 1계층 OSS
- source, resolver, builder를 제공하는 순수 기능 계층

## 목적

- 타입 안전한 정책 키, 설정 source, resolver, builder primitive를 1계층에 둔다.
- 현재 조직 표준 governance line인 `platform-governance`가 운영 정책 조회와 fail-fast 기준을 조립할 수 있게 한다.
- 같은 primitive를 바탕으로 다른 governance 2계층 line도 만들 수 있게 한다.

## 계층 원칙

- `policy-config`는 1계층 OSS다.
- `policy-config`는 정책 값을 읽고 해석하는 primitive를 제공한다.
- 정책 평가 엔진, 위반 대응, 운영 preset은 2계층 governance platform 책임이다.
- 서비스별 policy key와 정책 의미 hardcoding은 1계층 책임이 아니다.

## 모듈 기준

- `policy-config-contracts`
- `policy-config-core`
- `policy-config-builder`

## 포함해야 할 것

- 타입 안전한 policy key 모델
- 설정 source 계약
- resolver
- 타입 변환
- 기본값, alias, validation primitive
- resolver 조립 builder
- source operational status 표현

## 포함하지 말아야 할 것

- governance decision engine
- violation handler
- 서비스별 policy key catalog
- Spring Boot starter 조립
- audit 기록 orchestration

## 판정 기준

- 정책 값을 조회하고 타입 안전하게 해석하면 `policy-config` 책임이다.
- 조회한 정책으로 운영 결정을 내리고 위반을 처리하면 2계층 governance platform 책임이다.
