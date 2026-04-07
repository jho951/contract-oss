# CONTRACT_SYNC

이 문서는 `oss-contract`를 기준으로 1계층 OSS와 2계층 platform 문서를 동기화하는 규격이다.

## 목적

- 계약의 단일 진실원천을 유지한다.
- OSS와 platform의 책임 경계를 일관되게 맞춘다.
- 구현 레포가 제각각 다른 설명을 갖지 않도록 한다.

## 기준 저장소

- `oss-contract`: OSS와 platform 사이의 계약 SOT

## 동기화 대상

- 1계층 OSS 목록
- 1계층 OSS의 실제 역할
- 2계층 platform의 책임
- 의존 방향 규칙
- 공통 계약 범위

## 문서의 책임

### `oss-contract`에서 정의하는 것

- OSS 배포와 계약 기준
- 보안 계약
- 에러 계약
- 환경변수 계약
- OpenAPI 계약
- OSS/Platform 경계 규칙

### 각 OSS 레포에서 정의하는 것

- 해당 OSS의 구현
- 프레임워크 연동
- 내부 모듈 구조
- 운영 세부사항

### 각 platform 레포에서 정의하는 것

- 실제 서비스가 사용하는 공통 기반 구현
- OSS 모듈을 묶는 방식
- platform 내부 구현
- 서비스가 직접 소비하는 조립된 API 경계

## 현재 계층 정의

- 1계층 OSS: `auth`, `ip-guard`, `rate-limiter`, `audit-log`, `policy-config`, `plugin-policy-engine`, `file-storage`, `notification`
- 2계층 platform: `platform-security`, `platform-governance`, `platform-resource`

## 현재 역할 기준

- `auth`: 인증 처리, principal/token/session
- `ip-guard`: IP 허용/차단
- `rate-limiter`: 요청 속도 제한
- `audit-log`: 구조화 감사 로그
- `policy-config`: 정책 키/설정 소스 조회
- `plugin-policy-engine`: 정책 조합/평가
- `file-storage`: 파일 저장 추상화
- `notification`: 일반 알림 추상화, 메시지 모델, 전달 채널 조합

## 책임 수준 요약

- 1계층 OSS는 기능 구현과 published artifact 제공이 책임이다.
- 2계층 platform은 1계층 OSS를 조립해 3계층이 쉽게 가져다 쓸 수 있는 integration API를 제공하는 것이 책임이다.

## 동기화 절차

1. 이 레포의 `registry/*` 문서를 먼저 갱신한다.
2. 변경된 책임 경계에 맞춰 각 대상 레포의 README나 내부 문서를 갱신한다.
3. `oss-contract`와 대상 레포의 문구가 일치하는지 확인한다.
4. breaking change가 있으면 버전 또는 이행 문서를 갱신한다.
5. 변경 사유와 영향 범위를 기록한다.

## 변경 종류별 규칙

### 1. OSS 역할이 바뀌는 경우

- `registry/layer1-status.md`
- `registry/layer2-status.md`

를 함께 갱신한다.

### 2. platform 책임이 바뀌는 경우

- `registry/layer2-status.md`

를 함께 갱신한다.

### 3. 동기화 절차가 바뀌는 경우

- `registry/layer1-status.md`
- `registry/layer1-gradle-properties.md`
- `registry/layer1-ci-cd.md`
- `registry/layer1-maven-central.md`
- `registry/layer1-checklist.md`
- `registry/layer2-status.md`

를 함께 갱신한다.

## 동기화 원칙

- 문서는 구현보다 먼저 맞춘다.
- 구현 레포는 `oss-contract`의 문구를 거스르지 않는다.
- 애매하면 더 좁은 책임으로 자른다.
- 플랫폼끼리는 직접 의존하지 않는다.

## 상태 기록 템플릿

각 대상 레포에는 아래 상태를 남긴다.

- 기준 문서: `oss-contract`
- 대상 문서: 레포별 README 또는 계약 문서
- 마지막 동기화 일자
- 반영된 변경 요약
- 남은 작업
