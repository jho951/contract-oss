# platform-integrations Standard

이 문서는 `platform-integrations`가 L5 목표 구조에서 어떤 책임을 가져야 하는지 고정한다.

## 적용 범위

- 이 문서는 현재 조직이 운영하는 integrations 2계층 line으로서의 `platform-integrations` 기준을 정의한다.
- 이것이 2계층 outbound platform의 유일한 형태라는 뜻은 아니다.
- 다른 팀이나 프로젝트도 같은 1계층 OSS (`notification`)를 사용해 다른 outbound 2계층 line을 만들 수 있다.
- 다만 서비스는 raw OSS 대신 자신이 선택한 outbound platform line의 contract를 소비해야 한다.

## 역할

- 알림과 외부 연동과 outbound delivery 플랫폼
- 서비스 바깥으로 나가는 전달 흐름을 표준화하는 계층

## 목적

- 서비스마다 메일, 문자, 푸시, webhook, 외부 연동 코드를 따로 만들지 않게 한다.
- notification 모델, retry, idempotency, outbound error 표준을 현재 조직 표준 방식으로 제공한다.
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

## 현재 main 기준 public surface

- `platform-integrations-api`
- `platform-integrations-notification-adapter`
- `platform-integrations-autoconfigure`
- `platform-integrations-starter`
- 서비스-facing outbound 계약은 현재 `platform-integrations` line에서 `PlatformOutboundSender`를 사용한다.
- raw `NotificationDispatcher`는 adapter/autoconfigure 안에서만 알고, 서비스는 platform-owned outbound contract만 본다.

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

## 검증 기준

- `verifyPublishedSurface`는 outbound API, adapter, autoconfigure, starter가 publish surface에 포함되는지 확인해야 한다.
- `verifyStarterContract`는 서비스가 starter 하나로 outbound delivery 진입점을 받을 수 있는지 확인해야 한다.
- `verifyConsumerConformance`는 sample consumer가 raw notification OSS를 직접 붙이지 않아도 되는지 확인해야 한다.
- `verifyStage5Contract`는 public surface에 1계층 outbound 타입이 새지 않았는지 확인해야 한다.

## 운영 기준

- 실패 재시도, dead-letter, idempotency, provider fallback 같은 운영 기준은 `platform-integrations`에서 표준화한다.
