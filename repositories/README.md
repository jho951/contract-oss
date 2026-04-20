# Repository

## 역할

- GitHub URL과 최신 기준 버전을 기록한다.
- 책임과 공개 모듈 범위를 기록한다.
- 현재 문서, 운영 파일, 정리 후보를 기록한다.
- 최신 기준 버전은 원격 `main`의 `gradle.properties` `release_version`을 우선한다.
- platform 레포가 1계층을 소비하는 exact pin은 레포별 상태 문서의 `현재 version pin`에 별도로 기록한다.

## 경계

- 현재 레포 카탈로그와 점검 상태를 관리합니다.
- 문서, build, publish 구조 기준은 `registry/layer1` 또는 `registry/layer2`에서 관리합니다.
- 상세 코드 구현 관련 문서는 구현 레포 `docs/*`에서 관리합니다.

## 문서

- [layer1](layer1/README.md): 1계층 OSS 레포
- [layer2](layer2/README.md): 2계층 platform 레포
