# 1계층 레포 현황

현재 1계층 OSS는 아래와 같다.

- `auth`
- `ip-guard`
- `rate-limiter`
- `audit-log`
- `policy-config`
- `plugin-policy-engine`
- `file-storage`
- `notification`

## 기본 원칙

- 계약은 `oss-contract`가 먼저다.
- 구현은 계약을 거스르지 않는다.
- 문서는 구현보다 먼저 맞춘다.
- 1계층 OSS는 모두 필요한 인프라로 본다.
- 특정 OSS를 기준점으로 삼지 않는다.

## 책임

- 1계층 OSS는 기능 구현과 공개 artifact 발행 책임을 가진다.
- 1계층 OSS는 직접 소비 대상이 아니다.

## 반영 기준

- 1계층 OSS 변경은 해당 OSS의 build / publish 흐름까지 함께 본다.
- 문서, build, workflow는 같은 release 단위로 맞춘다.
- 한 번에 한 레포를 반영한다.
- 큰 구조 변경은 모듈 변경과 문서 변경을 분리할 수 있다.
- 레포별 반영 순서는 상황에 따라 조정할 수 있다.

## 접근 / 검증

1. 레포 존재 여부를 확인한다.
2. 읽기 접근 가능 여부를 확인한다.
3. 쓰기 접근 가능 여부를 확인한다.
4. 필요 시 로컬 clone으로 문서를 검증한다.
5. 접근 권한이 확인되기 전에는 실제 반영을 시도하지 않는다.

## 로컬 적용 방식

- 먼저 문서를 로컬에서 정리한다.
- 그다음 대상 레포와 line-by-line 비교한다.
- 차이가 있으면 patch 단위로 반영한다.
- 필요한 경우 로컬 clone을 이용해 검증한다.

## 실패 시 대응

- 파일 하나씩 반영이 꼬이면 `sync-final`과 대상 레포를 line-by-line 비교한다.
- 모듈명이 다르면 `settings.gradle`부터 고친다.
- publish가 실패하면 `build.gradle`과 secrets를 먼저 확인한다.

## 적용 기준

- `sync-final`은 최종 동기화 기준 문서 집합이다.
- `sync-drafts`는 초안이다.
- `sync-templates`는 생성 템플릿이다.
- 문서 외 산출물이 생기면 제거한다.

## 규칙

- 공통 계약은 `oss-contract`에서만 정의한다.
- 1계층 OSS는 기능 책임만 갖는다.
- publish 가능한 artifact 경계만 레포 책임으로 둔다.

## 기록 규칙

각 레포 반영 시 아래를 기록한다.

- 기준 문서
- 대상 레포
- 반영한 파일
- 반영 일자
- tag 버전
- 남은 작업
