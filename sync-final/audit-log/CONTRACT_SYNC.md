# CONTRACT_SYNC - audit-log

## 기준

- 기준 SOT: `oss-contract`
- 서비스 계약 기준: `service-contract`
- 대상 레포: `audit-log`

## 확인된 역할

- 구조화된 감사 로그 공통 모듈
- actor, occurredAt, clientIp, action, resource, result 중심
- Spring Boot starter 제공

## 반영 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `build.gradle`
- `settings.gradle`
- `.github/workflows/publish.yml`
