# platform-governance audit-log

`audit-log`는 `platform-governance`의 감사 로그 구현 레포다.

## 책임

- 구조화된 감사 로그 기록
- actor / occurredAt / clientIp / action / resource / result 표준화
- 보안 감사와 운영 추적 재사용
- Spring 연동

## 권장 모듈

- `audit-log-api`
- `audit-log-core`
- `audit-log-autoconfigure`
- `audit-log-spring-boot-starter`
- `audit-log-common-test`

## 모듈 설명

- `audit-log-api`: 감사 인터페이스
- `audit-log-core`: 표준 이벤트 모델과 sink
- `audit-log-autoconfigure`: Spring 자동 구성
- `audit-log-spring-boot-starter`: 소비 진입점
- `audit-log-common-test`: 테스트 지원

## 제외 범위

- 인증 token
- 정책 엔진
- 파일 저장
- 서비스 비즈니스 로직

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)
5. [docs/event-schema.md](docs/event-schema.md)
