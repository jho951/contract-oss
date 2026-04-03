# CONTRACT_SYNC - ip-guard

이 문서는 `ip-guard` 레포에 반영할 동기화 기준이다.

## 기준

- 기준 SOT: `oss-contract`
- 서비스 계약 기준: `service-contract`
- 대상 레포: `ip-guard`

## 확인된 역할

- IP 허용/차단 라이브러리
- core와 Spring Boot 연동 분리
- 요청 진입 보안 제어

## 동기화할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`

## 문구 기준

- `ip-guard`는 `platform-security`의 IP 접근 제어 구현 레포다.
- `ip-guard`는 요청 진입 보안을 담당한다.
- `ip-guard`는 인증, 정책, 감사, 저장 책임을 가지지 않는다.

