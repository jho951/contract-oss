# policy-config

## 계층

- 1계층 OSS
- `platform-governance`로 흡수될 기준 레포

## 상태

- 존재

## 소유 기준

- `oss-contract`
- `sync-final/policy-config/CONTRACT_SYNC.md`

## 역할

- 환경변수 조회
- System Properties 조회
- `.properties` 조회
- `Map` 기반 조회
- 정책 키 조회
- Spring 연동

## 현재

- 멀티모듈 governance OSS
- Maven Central 배포 대상
- tag 기반 publish 사용

## 모듈

- `policy-config-core`
- `policy-config-spring`
- `policy-config-spring-boot-starter`
- `policy-config-common-test`

## 목표

- `platform-governance`의 설정 조회 표준 구현
- 정책 키 조회와 설정 소스 해석을 분리
- core / spring / starter 골격 유지

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

- [sync-final/policy-config/CONTRACT_SYNC.md](../sync-final/policy-config/CONTRACT_SYNC.md)

