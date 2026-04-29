# rate-limiter Standard

이 문서는 `rate-limiter` 1계층 OSS의 표준 책임과 경계를 고정한다.

## 역할

- 요청 제한 key, plan, quota, decision primitive를 제공하는 1계층 OSS
- 제한 계산과 storage SPI를 제공하는 순수 기능 계층

## 목적

- rate limit 계산 primitive와 외부 저장소 연동 SPI를 1계층에 둔다.
- 현재 조직 표준 security line인 `platform-security`가 rate limit 집행을 보안 runtime에 조립할 수 있게 한다.
- 같은 primitive를 바탕으로 다른 security 2계층 line도 만들 수 있게 한다.

## 계층 원칙

- `rate-limiter`는 1계층 OSS다.
- `rate-limiter`는 제한 계산과 storage SPI를 제공하고 서비스 보안 체인 조립은 소유하지 않는다.
- 서비스 role preset, endpoint별 기본 제한, 실패 응답 표준화는 2계층 security platform 책임이다.
- 특정 Redis key convention이나 서비스별 plan policy hardcoding은 1계층 책임이 아니다.

## 모듈 기준

- `rate-limiter-core`
- `rate-limiter-spi`

## 포함해야 할 것

- rate limit key 모델
- plan, quota, window 모델
- allow/deny decision 모델
- policy 평가 primitive
- 외부 counter/storage 연동용 SPI

## 포함하지 말아야 할 것

- Spring Security filter 조립
- gateway 또는 service role preset 조립
- 특정 서비스별 Redis key 규칙
- IP guard, 인증, audit 처리
- HTTP 실패 응답 writer

## 판정 기준

- 제한 정책을 계산하고 decision을 반환하면 `rate-limiter` 책임이다.
- 어떤 요청에 어떤 preset과 실패 응답으로 적용할지 정하면 2계층 security platform 책임이다.
