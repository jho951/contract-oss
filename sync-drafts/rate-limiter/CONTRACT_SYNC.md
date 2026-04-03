# CONTRACT_SYNC - rate-limiter

이 문서는 `rate-limiter` 레포에 반영할 동기화 기준이다.

## 기준

- 기준 SOT: `oss-contract`
- 서비스 계약 기준: `service-contract`
- 대상 레포: `rate-limiter`

## 확인된 역할

- 요청 속도 제한 라이브러리
- IP / 사용자 ID / API 키 기준 제한
- in-memory, Redis, Spring Boot 지원

## 동기화할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`

## 문구 기준

- `rate-limiter`는 `platform-security`의 요청 속도 제한 구현 레포다.
- `rate-limiter`는 서비스 진입점의 과도한 호출을 제어한다.
- `rate-limiter`는 인증, 정책, 감사, 저장 책임을 가지지 않는다.

