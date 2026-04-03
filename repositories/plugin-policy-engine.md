# plugin-policy-engine

## 계층

- 1계층 OSS
- `platform-governance`로 흡수될 기준 레포

## 상태

- 존재

## 소유 기준

- `oss-contract`
- `sync-final/plugin-policy-engine/CONTRACT_SYNC.md`

## 역할

- rollout 평가
- targeting 평가
- variant 선택
- 정책 조합
- Spring 연동

## 현재

- 멀티모듈 governance OSS
- Maven Central 배포 대상
- tag 기반 publish 사용

## 모듈

- `plugin-policy-engine-core`
- `plugin-policy-engine-spring`
- `plugin-policy-engine-spring-boot-starter`
- `plugin-policy-engine-common-test`

## 목표

- `platform-governance`의 정책 평가 엔진 표준 구현
- policy-config와의 책임 경계 유지
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

- [sync-final/plugin-policy-engine/CONTRACT_SYNC.md](../sync-final/plugin-policy-engine/CONTRACT_SYNC.md)

