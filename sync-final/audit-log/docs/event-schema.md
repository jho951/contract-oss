# Event Schema

`audit-log`는 구조화된 감사 이벤트를 표준 필드로 기록한다.

## 표준 필드

- actor
- occurredAt
- clientIp
- action
- resource
- result

## 기록 원칙

- 이벤트는 사람이 읽을 수 있어야 한다.
- 보안 감사와 운영 추적 모두 같은 스키마를 사용한다.
- 인증, 정책, 저장 책임과 분리한다.

## 제외 범위

- 토큰 발급
- 정책 키 조회
- 파일 저장
- 서비스 비즈니스 로직
