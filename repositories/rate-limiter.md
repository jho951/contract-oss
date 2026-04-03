# rate-limiter

## 계층

- 1계층 OSS
- `platform-security`로 흡수될 기준 레포

## 상태

- 존재

## 소유 기준

- `oss-contract`
- `sync-final/rate-limiter/CONTRACT_SYNC.md`

## 역할

- IP / 사용자 ID / API 키 기준 rate limit
- in-memory 제한
- Redis 기반 분산 제한
- Spring 연동

## 현재

- 멀티모듈 보안 OSS
- Maven Central 배포 대상
- tag 기반 publish 사용

## 모듈

- `rate-limiter-core`
- `rate-limiter-redis`
- `rate-limiter-spring`
- `rate-limiter-spring-boot-starter`
- `rate-limiter-common-test`

## 목표

- `platform-security`의 요청량 제어 표준 구현
- auth / ip-guard와 같은 Gradle 골격 유지
- 분산 rate limit을 표준화

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

- [sync-final/rate-limiter/CONTRACT_SYNC.md](../sync-final/rate-limiter/CONTRACT_SYNC.md)

