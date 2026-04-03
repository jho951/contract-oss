# 운영 규칙

이 문서는 `oss-contract`를 기준으로 1계층 OSS와 관련 레포를 운영하는 규칙을 정의한다.

## 목적

- 배포와 반영의 판단 기준을 하나로 만든다.
- 문서와 구현의 동기화 순서를 고정한다.
- 릴리즈와 롤백을 예측 가능하게 만든다.

## 1. 기본 원칙

- 계약은 `oss-contract`가 먼저다.
- 서비스 계약은 `service-contract`가 먼저다.
- 구현은 계약을 거스르지 않는다.
- 문서는 구현보다 먼저 맞춘다.
- 실제 반영은 로컬 검증 후 수행한다.

## 2. 배포 원칙

### 2.1 1계층 OSS

- 1계층 OSS는 모두 Maven Central 배포 대상이다.
- 배포는 tag 기반이다.
- `publish.yml`은 tag push에서만 동작한다.
- 일반 branch push는 배포하지 않는다.

### 2.2 좌표 규칙

- `groupId`: `io.github.jho951`
- `artifactId`: 레포명 또는 모듈명
- `version`: tag와 일치

### 2.3 버전 규칙

- release tag는 `vX.Y.Z` 형식을 기본으로 한다.
- tag의 버전과 artifact version은 같게 둔다.
- publish 시 `releaseVersion` property를 사용한다.
- breaking change는 major version을 올린다.
- snapshot은 내부 검증용으로만 쓴다.

### 2.4 배포 자격

- 테스트가 통과해야 한다.
- signing이 가능해야 한다.
- Maven Central credentials가 있어야 한다.

## 3. 반영 원칙

### 3.1 반영 순서

1. `oss-contract` 문서 갱신
2. 대상 레포의 `CONTRACT_SYNC.md` 확인
3. 대상 레포의 `README.md` 확인
4. 대상 레포의 `docs/` 확인
5. 대상 레포의 `build.gradle` / `settings.gradle` 확인
6. 대상 레포의 `publish.yml` 확인
7. 로컬 diff 검증
8. 반영

### 3.2 반영 단위

- 한 번에 한 레포를 반영한다.
- 가능한 한 문서 / build / workflow를 하나의 논리 변경으로 묶는다.
- 큰 구조 변경은 모듈 변경과 문서 변경을 분리할 수 있다.

### 3.3 승인 기준

- 쓰기 권한이 있으면 직접 반영한다.
- 쓰기 권한이 없으면 patch와 초안만 준비한다.
- 브랜치 보호가 있으면 PR로 반영한다.

## 4. 접근 규칙

- 레포 존재 여부를 먼저 확인한다.
- `git ls-remote`로 읽기 가능 여부를 확인한다.
- `git clone`으로 로컬 검증 가능 여부를 확인한다.
- `git push --dry-run`으로 쓰기 가능 여부를 확인한다.
- 접근 권한이 확인되기 전에는 실제 반영을 시도하지 않는다.

## 5. 롤백 규칙

- 배포 후 문제가 생기면 이전 tag로 되돌린다.
- 문서만 문제가 있으면 다음 patch에서 수정한다.
- 계약이 잘못되면 new tag로 수정하고 이전 tag를 유지한다.
- breaking change를 되돌릴 때는 새 minor/patch 릴리즈로 정정한다.

## 6. 표준 작업 흐름

1. `oss-contract` 갱신
2. 레포 접근 확인
3. `sync-final` 또는 patch 준비
4. 로컬 검증
5. PR 또는 direct push
6. tag 생성
7. publish
8. 반영 결과 기록

### 6.1 실행 순서 문서

- 실제 레포에 커밋하고 push/tag를 하는 구체적 순서는 [release-execution-order.md](release-execution-order.md)를 따른다.
- `final-apply-order.md`는 무엇을 먼저 반영할지의 우선순위이고, `release-execution-order.md`는 어떻게 커밋하고 배포할지의 실행 순서다.

## 7. 기록 규칙

각 레포 반영 시 아래를 기록한다.

- 기준 문서
- 대상 레포
- 반영한 파일
- 반영 일자
- tag 버전
- 남은 작업

## 8. 예외 규칙

- `notification`은 아직 분류 보류다.
- 플랫폼 내부 문서는 플랫폼 레포에만 둔다.
- 서비스 내부 문서는 `service-contract`와 서비스 레포에 둔다.
- 계약과 구현이 충돌하면 계약을 먼저 고친다.
