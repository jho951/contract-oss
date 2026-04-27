# L5 전환 순서

이 문서는 [l5-target-architecture.md](l5-target-architecture.md)에 적은 목표 구조로 실제로 옮겨가는 순서를 정리한다.

서비스별 실제 정리 기준은 [l5-service-migration-checklist.md](l5-service-migration-checklist.md)에서 따로 관리한다.

## 핵심 원칙

- 서비스에서 OSS 직접 참조를 금지한다.
- 서비스에서 service-owned filter, service-owned audit adapter, service-owned storage helper, service-owned notification sender를 제거한다.
- 플랫폼 간 순환 의존을 금지한다.
- 현재 동작을 살리기 위한 임시 compat 코드는 플랫폼 안으로만 넣고, 서비스에는 남기지 않는다.
- 새 구조의 public contract가 먼저 나오고, 구현은 그 뒤에 붙는다.

## 큰 순서

```text
1. 책임 고정
2. public contract 고정
3. 서비스의 OSS 직접 참조 차단
4. 플랫폼별 실행 흐름 이관
5. 서비스 얇게 만들기
6. 중복/레거시 삭제
7. contract test와 smoke test 고정
```

## 1. 책임 먼저 고정

- `platform-security`는 인증, 인가, 필터, JWT, 세션, 권한 진입점, ingress 집행을 소유한다.
- `platform-governance`는 audit, policy config, policy engine, violation handling, 운영 통제를 소유한다.
- `platform-resource`는 resource lifecycle, metadata, storage abstraction, access, kind policy를 소유한다.
- `platform-integrations`는 notification, outbound delivery, 외부 연동 실행 표준을 소유한다.

## 2. public contract를 먼저 고정

- `platform-security` public API와 SPI 확정
- `platform-governance` public API와 SPI 확정
- `platform-resource` public API와 SPI 확정
- `platform-integrations` public API와 SPI 확정

## 3. 서비스의 OSS 직접 참조를 먼저 끊기

찾아야 할 것:

- 서비스에서 `oss-auth` 직접 사용
- 서비스에서 `oss-audit-log` 직접 사용
- 서비스에서 `oss-file-storage` 직접 사용
- 서비스에서 `oss-notification` 직접 사용
- 서비스에서 `oss-rate-limiter`, `oss-ip-guard`, `oss-policy-config`, `oss-plugin-policy-engine` 직접 사용

## 4. 플랫폼별 실행 흐름 이관

- `platform-security`: 로그인, JWT, 세션, 인증 실패 응답, SecurityContext
- `platform-governance`: audit, policy loading, policy engine, violation handling
- `platform-resource`: upload, download, delete, metadata, lifecycle
- `platform-integrations`: notification, retry, idempotency, outbound delivery

## 5. 서비스를 얇게 만들기

서비스에는 아래만 남겨야 한다.

- 도메인 모델
- 플랫폼 SPI 구현
- 플랫폼 설정
- 도메인과 플랫폼 연결 코드

## 6. 마지막에 지울 것

- 서비스별 JWT helper
- 서비스별 login helper
- 서비스별 audit formatter
- 서비스별 file upload helper
- 서비스별 mail sender
- 서비스별 retry worker
- service-owned compat adapter

## 7. 테스트 고정

- platform contract test
- starter boot smoke test
- sample consumer test
- cross-platform smoke test
