# 레포 적용 가이드

이 문서는 `oss-contract`의 문서를 실제 각 레포에 적용하는 방법을 정의한다.

## 기본 원칙

- 먼저 `repositories/*`에서 해당 레포의 현재/목표 상태를 확인한다.
- 다음으로 `sync-final/<repo>/`에서 반영할 최종 문구를 확인한다.
- 그다음 대상 레포에 실제 파일을 옮긴다.
- 마지막에 `CONTRACT_SYNC.md`와 `repositories/*`를 다시 갱신한다.

## 공통 적용 순서

각 레포는 아래 순서로 적용한다.

1. `README.md`
2. `CONTRACT_SYNC.md`
3. `settings.gradle`
4. `build.gradle`
5. `.github/workflows/publish.yml`
6. `docs/README.md`
7. `docs/architecture.md`
8. `docs/modules.md`
9. `docs/extension-guide.md`
10. 추가 문서

## 1계층 OSS 적용 방법

### 1. 레포 확인

- `repositories/<repo>.md`를 읽어서 현재/목표 상태를 확인한다.
- `sync-final/<repo>/`가 있는지 확인한다.
- 대상 레포의 현재 구조를 본다.

### 2. 브랜치 생성

- 예시 브랜치: `docs/oss-contract-sync`
- 변경이 크면 별도 브랜치명을 붙인다.

### 3. 파일 반영

- `sync-final/<repo>/README.md`를 대상 `README.md`로 반영한다.
- `sync-final/<repo>/CONTRACT_SYNC.md`를 대상 레포 루트에 둔다.
- `sync-final/<repo>/build.gradle`과 `settings.gradle`을 루트에 둔다.
- `sync-final/<repo>/.github/workflows/publish.yml`을 workflow로 둔다.
- `sync-final/<repo>/docs/*`를 대상 `docs/`로 둔다.

### 4. 검증

- 모듈 이름이 `registry/layer1-structure.md`와 맞는지 확인한다.
- 배포 규칙이 `registry/operation-rules.md`와 맞는지 확인한다.
- tag 기반 publish인지 확인한다.
- Maven Central 좌표가 맞는지 확인한다.

### 5. 반영

- 쓰기 권한이 있으면 직접 push한다.
- 쓰기 권한이 없으면 patch 또는 PR로 전달한다.

## 2계층 platform 적용 방법

- 아직 platform 레포가 없으면 문서만 유지한다.
- 플랫폼 레포가 생기면 `repositories/platform-*.md`를 기준으로 계약 문서를 만든다.
- platform은 1계층 OSS를 흡수하는 구현 레포이므로, 직접 OSS 구현 문서를 복제하지 않는다.

## 3계층 service 적용 방법

- 실제 서비스 레포는 `repositories/service-contract.md`를 기준으로 맞춘다.
- `service-contract`가 먼저다.
- 서비스는 플랫폼을 조립하는 레포이므로, 플랫폼 내부 구현을 복제하지 않는다.

## `notification`

- `notification`은 현재 보류다.
- 코드가 생기기 전에는 적용하지 않는다.

## 실패 시 대응

- 파일 하나씩 반영이 꼬이면 `sync-final`과 대상 레포를 line-by-line 비교한다.
- 모듈명이 다르면 `settings.gradle`부터 고친다.
- publish가 실패하면 `build.gradle`과 secrets를 먼저 확인한다.

## 기록

적용 후에는 아래를 갱신한다.

- `repositories/<repo>.md`
- `sync-final/<repo>/CONTRACT_SYNC.md`
- `registry/final-apply-order.md`
- 필요 시 `registry/operation-rules.md`

