# ip-guard

## 계층

- 1계층 OSS
- `platform-security`로 흡수될 기준 레포

## 상태

- 존재

## 소유 기준

- `oss-contract`
- `sync-final/ip-guard/CONTRACT_SYNC.md`

## 역할

- IP 허용/차단
- 요청 진입 제어
- core 판단 로직
- Spring 연동

## 현재

- 멀티모듈 보안 OSS
- Maven Central 배포 대상
- tag 기반 publish 사용

## 모듈

- `ip-guard-core`
- `ip-guard-spring`
- `ip-guard-spring-boot-starter`
- `ip-guard-common-test`

## 목표

- `platform-security`의 IP 접근 제어 표준 구현
- auth와 동일한 Gradle/publish 골격
- 보안 진입 제어의 일관된 문서화

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

- [sync-final/ip-guard/CONTRACT_SYNC.md](../sync-final/ip-guard/CONTRACT_SYNC.md)

