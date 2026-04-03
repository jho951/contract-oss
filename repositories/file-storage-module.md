# file-storage-module

## 계층

- 1계층 OSS
- 실제 GitHub 레포명은 `file-storage`이며, 공개 역할명은 `file-storage-module`이다.

## 상태

- 존재
- 실제 레포: `https://github.com/jho951/file-storage`

## 소유 기준

- `oss-contract`
- `sync-final/file-storage-module/CONTRACT_SYNC.md`
- 실제 반영 대상 레포: `file-storage`

## 역할

- 파일 저장 인터페이스
- 저장/조회 추상화
- storage path 규칙

## 현재

- 멀티모듈 storage OSS
- Maven Central 배포 대상
- tag 기반 publish 사용

## 모듈

- `file-storage-api`
- `file-storage-core`
- `file-storage-spring`
- `file-storage-spring-boot-starter`
- `file-storage-common-test`

## 목표

- `platform-storage`의 파일 저장 표준 구현
- API / core / spring / starter 패턴 유지
- 저장 추상화와 구현체 교체를 분리

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

- [sync-final/file-storage-module/CONTRACT_SYNC.md](../sync-final/file-storage-module/CONTRACT_SYNC.md)

