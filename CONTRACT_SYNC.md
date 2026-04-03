# CONTRACT_SYNC

이 문서는 `oss-contract`를 기준으로 1계층 OSS, 2계층 platform, 3계층 service 문서를 동기화하는 규격이다.

## 목적

- 계약의 단일 진실원천을 유지한다.
- OSS, platform, service의 책임 경계를 일관되게 맞춘다.
- 구현 레포가 제각각 다른 설명을 갖지 않도록 한다.

## 기준 저장소

- `oss-contract`: OSS와 platform 사이의 계약 SOT
- `service-contract`: 실제 서비스 서버와 platform 사이의 계약 SOT

## 동기화 대상

- 1계층 OSS 목록
- 1계층 OSS의 실제 역할
- 2계층 platform의 책임
- 3계층 service의 책임
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

### `service-contract`에서 정의하는 것

- 실제 서비스 서버의 계약
- 서비스 요청/응답 규격
- 서비스 간 인터페이스
- 서비스별 환경변수와 OpenAPI 규약

### 각 OSS 레포에서 정의하는 것

- 해당 OSS의 구현
- 프레임워크 연동
- 내부 모듈 구조
- 운영 세부사항

### 각 platform 레포에서 정의하는 것

- 실제 서비스가 사용하는 공통 기반 구현
- OSS 모듈을 묶는 방식
- platform 내부 구현

### 각 service 레포에서 정의하는 것

- 실제 고객/업무 기능
- platform 조합 방식
- 서비스 고유 API와 흐름

## 현재 계층 정의

- 1계층 OSS: `auth`, `ip-guard`, `rate-limiter`, `audit-log`, `policy-config`, `plugin-policy-engine`, `file-storage-module`, `notification`
- 2계층 platform: `platform-security`, `platform-governance`, `platform-storage`
- 3계층 service: 주문, 예약, 정산 같은 실제 서비스

## 현재 역할 기준

- `auth`: 인증 처리, principal/token/session
- `ip-guard`: IP 허용/차단
- `rate-limiter`: 요청 속도 제한
- `audit-log`: 구조화 감사 로그
- `policy-config`: 정책 키/설정 소스 조회
- `plugin-policy-engine`: 정책 조합/평가
- `file-storage-module`: 파일 저장 추상화
- `notification`: 작성 전

## 동기화 절차

1. 이 레포의 `registry/*` 문서를 먼저 갱신한다.
2. 변경된 책임 경계에 맞춰 각 대상 레포의 README나 내부 문서를 갱신한다.
3. `oss-contract`와 대상 레포의 문구가 일치하는지 확인한다.
4. breaking change가 있으면 버전 또는 이행 문서를 갱신한다.
5. 변경 사유와 영향 범위를 기록한다.

## 변경 종류별 규칙

### 1. OSS 역할이 바뀌는 경우

- `registry/current-oss.md`
- `registry/observed-roles.md`
- `registry/mapping.md`
- `registry/repo-roles.md`

를 함께 갱신한다.

### 2. platform 책임이 바뀌는 경우

- `registry/future-platforms.md`
- `registry/dependency-rules.md`
- `registry/repo-roles.md`

를 함께 갱신한다.

### 3. service 경계가 바뀌는 경우

- `registry/service-layer.md`
- `registry/service-contract.md`
- `registry/dependency-rules.md`

를 함께 갱신한다.

## 동기화 원칙

- 문서는 구현보다 먼저 맞춘다.
- 구현 레포는 `oss-contract`의 문구를 거스르지 않는다.
- 애매하면 더 좁은 책임으로 자른다.
- 플랫폼끼리는 직접 의존하지 않는다.
- 서비스는 플랫폼을 조립해서 쓴다.

## 상태 기록 템플릿

각 대상 레포에는 아래 상태를 남긴다.

- 기준 문서: `oss-contract`
- 대상 문서: 레포별 README 또는 계약 문서
- 마지막 동기화 일자
- 반영된 변경 요약
- 남은 작업

