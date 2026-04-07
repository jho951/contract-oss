# Delivery Model

`notification`의 기본 전달 모델은 메시지, 채널, dispatcher로 구성된다.

## 흐름

1. 서비스 또는 플랫폼 코드가 `NotificationMessage`를 만든다.
2. `NotificationDispatcher`가 메시지를 받는다.
3. dispatcher는 등록된 채널들로 메시지를 전달한다.
4. 결과는 `NotificationDispatchResult`로 반환된다.

## 원칙

- 메시지에는 수신자, 제목, 본문, 우선순위가 포함된다.
- 채널은 전달 수단을 의미한다.
- dispatcher는 채널별 실패를 격리할 수 있어야 한다.

## 기본 동작

- 채널이 없으면 noop 결과를 반환한다.
- 하나의 채널 실패가 전체 메시지 실패와 같지는 않다.
- 테스트에서는 인메모리 채널을 사용한다.

## 채널 범위

- `notification-core`는 인메모리/조합 dispatcher를 제공한다.
- `notification-console`은 운영 확인용 콘솔 출력 어댑터다.
- `notification-email`은 SMTP 기반 이메일 어댑터다.
- `notification-webhook`은 범용 HTTP 전달 어댑터다.
- `notification-slack`은 Slack webhook 어댑터다.
