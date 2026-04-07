# API Model

`notification-api`는 메시지와 전달 결과의 공통 계약을 제공한다.

## 핵심 타입

- `NotificationMessage`
- `NotificationDispatcher`
- `NotificationChannel`
- `NotificationDelivery`
- `NotificationDispatchResult`
- `NotificationDeliveryStatus`
- `NotificationErrorCode`
- `NotificationException`

## 모델 원칙

- 메시지 계약은 프레임워크와 분리한다.
- 전달 결과는 성공과 실패를 구분한다.
- 실패는 오류 코드와 설명을 함께 제공한다.
- 호출자는 채널별 실패를 집계해서 처리할 수 있어야 한다.

## 제외 범위

- 채널 구현 세부사항
- transport client 설정
- Spring auto-configuration
- 서비스 비즈니스 정책
