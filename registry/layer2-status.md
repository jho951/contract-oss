# 2계층 플랫폼 현황

현재 2계층 platform은 아래와 같다.

- `platform-security`
- `platform-governance`
- `platform-resource`

## 의미

- 2계층은 1계층 OSS를 조립하는 private platform 레포다.
- 2계층은 소비자가 쉽게 조립할 수 있는 integration API를 제공한다.
- 2계층 API는 프레임워크 최종 진입점이 아니다.
- platform 분류는 책임 축으로 정한다.

## 기본 원칙

- 계약은 `oss-contract`가 먼저다.
- 구현은 계약을 거스르지 않는다.
- 문서는 구현보다 먼저 맞춘다.
- 특정 platform을 기준점으로 삼지 않는다.
- 2계층 platform은 1계층 published artifact를 exact version으로만 소비한다.
- 실제 반영은 로컬 검증 후 수행한다.

## 축 요약

| 축 | 포함 모듈 | 핵심 책임 |
| --- | --- | --- |
| Platform Security | `auth`, `ip-guard`, `rate-limiter` | 인증, 접근 통제, 요청 보호 |
| Platform Governance | `audit-log`, `policy-config`, `plugin-policy-engine` | 정책 관리, 정책 실행, 감사 추적 |
| Platform Resource | `file-storage`, `notification` | 파일 저장, 메시지 전달, 자원 전달 |

## 매핑

| 1계층 OSS | 2계층 platform |
| --- | --- |
| `auth`, `ip-guard`, `rate-limiter` | `platform-security` |
| `audit-log`, `policy-config`, `plugin-policy-engine` | `platform-governance` |
| `file-storage`, `notification` | `platform-resource` |

## 책임

- 2계층 platform은 조립, 정책 결합, 공통 설정, integration API 책임을 가진다.
- 2계층 platform은 OSS 내부 모듈이 아니라, 책임 축을 묶는 개념이다.

## 규칙

- 공통 계약은 `oss-contract`에서만 정의한다.
- 2계층 API는 소비자가 조립하기 쉬운 integration API여야 한다.
- dynamic version, version range, `latest.release`, `+` 참조는 금지한다.
- 한 번에 한 platform 레포를 반영한다.
- 문서, build, workflow는 같은 변경 단위로 묶는다.
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
- 의존성 반영이 꼬이면 `build.gradle`과 version pin을 먼저 확인한다.

## 적용 기준

- `sync-final`은 최종 동기화 기준 문서 집합이다.
- `sync-drafts`는 초안이다.
- `sync-templates`는 생성 템플릿이다.
- 문서 외 산출물이 생기면 제거한다.

## 기록 규칙

각 레포 반영 시 아래를 기록한다.

- 기준 문서
- 대상 레포
- 반영한 파일
- 반영 일자
- tag 버전
- 남은 작업
