# ip-guard Standard

이 문서는 `ip-guard` 1계층 OSS의 표준 책임과 경계를 고정한다.

## 역할

- IP 접근 제어 rule과 matching primitive를 제공하는 1계층 OSS
- IPv4, IPv6, CIDR, range, wildcard rule을 해석하는 순수 기능 계층

## 목적

- IP 접근 제어의 입력, 출력, 규칙 문법, 매칭 엔진을 1계층에 둔다.
- 현재 조직 표준 security line인 `platform-security`가 IP guard 정책을 runtime 보안 체인에 조립할 수 있게 한다.
- 같은 primitive를 바탕으로 다른 security 2계층 line도 만들 수 있게 한다.

## 계층 원칙

- `ip-guard`는 1계층 OSS다.
- `ip-guard`는 IP rule 평가 primitive를 제공하고 요청 필터 조립은 소유하지 않는다.
- trusted proxy CIDR 운영 정책과 gateway boundary 적용은 2계층 security platform 책임이다.
- 서비스별 allow/deny 운영 값과 rollout은 소비자 또는 2계층 platform 설정 책임이다.

## 모듈 기준

- `ip-guard-core`
- `ip-guard-spi`

## 포함해야 할 것

- IP rule 모델
- 입력과 출력 decision 모델
- IPv4, IPv6 single, CIDR, range, IPv4 wildcard 문법
- rule 파싱과 매칭
- 외부 rule source 연동용 SPI

## 포함하지 말아야 할 것

- Spring Security filter 조립
- gateway trusted header scrub/reinject
- 서비스별 IP policy hardcoding
- admin/internal preset 조립
- rate limit 또는 인증 처리

## 판정 기준

- IP 문자열과 rule을 해석하고 match/decision을 계산하면 `ip-guard` 책임이다.
- HTTP 요청 경계에서 IP guard를 언제 실행하고 실패 응답을 어떻게 쓸지 정하면 2계층 security platform 책임이다.
