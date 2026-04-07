# Channel Adapters

`notification`은 1계층 OSS로서 전달 수단별 어댑터를 분리한다.

## 포함 범위

- `notification-core`의 in-memory channel
- `notification-console`의 콘솔 출력 channel
- `notification-email`의 SMTP email channel
- `notification-webhook`의 HTTP webhook channel
- `notification-slack`의 Slack webhook channel

## 설계 원칙

- 어댑터는 메시지 계약을 변경하지 않는다.
- 어댑터는 전송 방식만 책임진다.
- 인증/정책/저장 책임은 포함하지 않는다.

## 사용 기준

- `notification-core`: 조합과 테스트
- `notification-console`: 로컬 확인, 디버깅, 샘플
- `notification-email`: 이메일 전송
- `notification-webhook`: 범용 외부 시스템 전송
- `notification-slack`: Slack 알림 전송

## 제외 범위

- 벤더 종속 SDK를 공통 계약으로 고정하는 것
- 큐, 재시도, DLQ, 스케줄링
- 서비스별 라우팅 규칙
