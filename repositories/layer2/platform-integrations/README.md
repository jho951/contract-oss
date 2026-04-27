# platform-integrations

## 목표 역할

- 알림과 외부 연동 outbound 플랫폼
- 메일, 문자, 푸시, webhook, 이벤트 발행 공통 실행 표준

## 주로 소비하는 OSS

- `notification`

## 플랫폼이 소유해야 할 것

- notification 표준 모델
- email, SMS, push, webhook provider 추상화
- 알림 템플릿 처리
- 발송 실패 재시도 정책
- 외부 연동 예외 표준화
- integration event 발행
- idempotency key 처리

## 서비스가 해야 하는 것

- 어떤 상황에 어떤 메시지를 보낼지 결정
- 어떤 템플릿을 쓸지 결정
- 어떤 도메인 이벤트를 outbound로 내보낼지 결정

## 서비스가 하지 말아야 하는 것

- 직접 메일 발송 구현
- 직접 SMS provider 호출
- 직접 재시도 로직 구현
- 서비스마다 알림 포맷 따로 정의

## 의존 방향

- `platform-integrations -> platform-governance`는 가능하다.
- `platform-integrations`는 다른 플랫폼의 내부 구현 owner가 아니다.
- outbound 실행은 소유하되, 도메인 의미와 발송 타이밍은 서비스가 owner다.
