# 의존 규칙

## 허용되는 방향

- 실제 서비스 서버 -> `platform-security`
- 실제 서비스 서버 -> `platform-governance`
- 실제 서비스 서버 -> `platform-storage`
- 각 platform -> `oss-contract`
- 각 service -> `service-contract`
- 실제 서비스 서버 -> `service-contract`

## 금지되는 방향

- `platform-security` -> `platform-governance`
- `platform-security` -> `platform-storage`
- `platform-governance` -> `platform-security`
- `platform-governance` -> `platform-storage`
- `platform-storage` -> `platform-security`
- `platform-storage` -> `platform-governance`

## 이유

- 플랫폼끼리 직접 얽히면 경계가 무너진다.
- 계약은 하나의 SOT여야 한다.
- 구현은 각 플랫폼이 독립적으로 가져간다.
- 실제 서비스의 기준은 `service-contract`에 있다.
- 서비스는 `service-contract` 기준의 서버 구현들이다.
- `service-contract`는 실제 서비스의 계약 SOT다.
