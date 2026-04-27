# platform-integrations Standard

이 문서는 `platform-integrations`가 L5 목표 구조에서 어떤 책임을 가져야 하는지 고정한다.

## 역할

- 알림과 외부 연동과 outbound delivery 플랫폼
- 서비스 바깥으로 나가는 전달 흐름을 표준화하는 계층

## 목적

- 서비스마다 메일, 문자, 푸시, webhook, 외부 연동 코드를 따로 만들지 않게 한다.
- notification 모델, retry, idempotency, outbound error 표준을 한 곳에 모은다.
- 서비스는 무엇을 보낼지 결정하고, 어떻게 보낼지는 platform이 소유하게 한다.

## 소유해야 할 것

- notification 표준 모델
- email, SMS, push, webhook provider 추상화
- 알림 템플릿 처리
- 발송 실패 재시도 정책
- 외부 연동 예외 표준화
- integration event 발행
- idempotency key 처리

## 1계층 조립 기준

- `notification`

## 포함해야 할 것

- outbound sender API와 SPI
- provider abstraction
- retry와 idempotency
- 공통 delivery result 모델
- typed properties

## 포함하지 말아야 할 것

- 서비스별 알림 문구 하드코딩
- 서비스별 발송 타이밍 판단
- 서비스별 비즈니스 이벤트 의미 정의
- 서비스별 외부 시스템 client 직접 구현

## 경계 규칙

- `platform-integrations`는 outbound 실행 표준의 owner다.
- 도메인 의미와 발송 타이밍은 서비스가 owner다.
- `platform-integrations`가 다른 플랫폼의 내부 구현을 직접 알면 안 된다.
- 필요하면 `platform-governance`의 audit, policy 기준을 소비할 수 있지만 순환 의존을 만들면 안 된다.

## 운영 기준

- 실패 재시도, dead-letter, idempotency, provider fallback 같은 운영 기준은 `platform-integrations`에서 표준화한다.
