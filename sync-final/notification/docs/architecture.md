# Architecture

`notification`은 메시지 모델과 전달 채널을 분리한다.

## 원칙

- 메시지 구조는 프레임워크와 독립적이어야 한다.
- 전달 채널은 여러 개일 수 있다.
- dispatcher는 채널 조합만 책임진다.
- Spring 연동은 바깥 어댑터에 둔다.

## 구성

- `notification-api`: 메시지와 전달 인터페이스
- `notification-core`: dispatcher와 기본 채널 구현
- `notification-console`: 콘솔 출력 어댑터
- `notification-email`: SMTP 이메일 어댑터
- `notification-webhook`: HTTP webhook 어댑터
- `notification-slack`: Slack webhook 어댑터
- `notification-spring`: Spring 자동 구성
- `notification-spring-boot-starter`: 애플리케이션 진입점
- `notification-common-test`: 테스트용 픽스처
