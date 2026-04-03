# 실행 순서

이 문서는 실제 레포에 표준을 반영할 때의 커밋, push, tag 순서를 정리한다.

## 목적

- 한 번에 너무 많은 레포를 건드리지 않도록 순서를 고정한다.
- 커밋 단위를 작게 유지해서 문제 발생 시 되돌리기 쉽게 만든다.
- `oss-contract`에서 만든 문서와 실제 레포 반영을 분리한다.

## 적용 대상

- `auth`
- `ip-guard`
- `rate-limiter`
- `audit-log`
- `policy-config`
- `plugin-policy-engine`
- `file-storage`

`notification`은 아직 작성 전이므로 제외한다.

## 권장 실행 순서

### 1단계: 보안 계층

1. `auth`
2. `ip-guard`
3. `rate-limiter`

### 2단계: 거버넌스 계층

4. `audit-log`
5. `policy-config`
6. `plugin-policy-engine`

### 3단계: 스토리지 계층

7. `file-storage`

## 레포별 커밋 단위

각 레포는 아래 단위로 나눠 커밋한다.

1. `CONTRACT_SYNC.md`
2. `README.md`
3. `docs/` 진입점과 경계 설명
4. `build.gradle` / `settings.gradle`
5. `.github/workflows/build.yml` 또는 `publish.yml`
6. 버전 규칙 반영

### 커밋 메시지 예시

- `docs: align auth with oss-contract`
- `build: adopt releaseVersion for file-storage`
- `ci: standardize publish workflow for audit-log`
- `docs: add CONTRACT_SYNC for ip-guard`

## push/tag 순서

### 문서 반영 후

1. `CONTRACT_SYNC.md`
2. `README.md`
3. `docs/`
4. `build.gradle`
5. `settings.gradle`
6. CI workflow

### 릴리즈 반영 후

1. 로컬에서 `./gradlew clean test`
2. 필요 시 `./gradlew publishToMavenLocal`
3. 커밋
4. `main` 또는 작업 브랜치 push
5. `vX.Y.Z` tag 생성
6. tag push
7. GitHub Actions `publish` 확인
8. Maven Central 확인

## 실제 운영 원칙

- 하나의 레포는 하나의 논리 변경으로 끝낸다.
- 버전과 태그는 항상 같이 움직인다.
- publish는 tag push에서만 한다.
- branch push는 검증만 한다.
- 먼저 문서를 맞추고, 그다음 build와 CI를 맞춘다.

## 기록 항목

각 반영 건마다 아래를 남긴다.

- 대상 레포
- 반영 커밋
- 태그 버전
- 검증 결과
- 남은 후속 작업

