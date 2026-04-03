# audit-log

## 계층

- 1계층 OSS
- `platform-governance`로 흡수될 기준 레포

## 상태

- 존재

## 소유 기준

- `oss-contract`
- `sync-final/audit-log/CONTRACT_SYNC.md`

## 역할

- 구조화된 감사 로그
- actor / occurredAt / clientIp / action / resource / result
- Spring 연동

## 현재

- 멀티모듈 governance OSS
- Maven Central 배포 대상
- tag 기반 publish 사용

## 모듈

- `audit-log-api`
- `audit-log-core`
- `audit-log-autoconfigure`
- `audit-log-spring-boot-starter`
- `audit-log-common-test`

## 목표

- `platform-governance`의 감사 표준 구현
- 공통 감사 필드의 단일 기준화
- api / core / autoconfigure / starter 패턴 유지

## 변경 포인트

- 루트 `build.gradle`
- `settings.gradle`
- `.github/workflows/publish.yml`
- `docs/`

## 배포

- Maven Central
- tag 기반 publish
- GitHub Actions `publish.yml`

## 동기화 기준

- [sync-final/audit-log/CONTRACT_SYNC.md](../sync-final/audit-log/CONTRACT_SYNC.md)

