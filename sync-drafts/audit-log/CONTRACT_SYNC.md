# CONTRACT_SYNC - audit-log

이 문서는 `audit-log` 레포에 반영할 동기화 기준이다.

## 기준

- 기준 SOT: `oss-contract`
- 서비스 계약 기준: `service-contract`
- 대상 레포: `audit-log`

## 확인된 역할

- 구조화된 감사 로그 공통 모듈
- actor, occurredAt, clientIp, action, resource, result 중심
- Spring Boot starter 제공

## 동기화할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`

## 문구 기준

- `audit-log`는 `platform-governance`의 감사 로그 구현 레포다.
- `audit-log`는 보안 감사와 운영 추적을 위한 표준 필드를 제공한다.
- `audit-log`는 인증, 정책 평가, 파일 저장 책임을 가지지 않는다.

