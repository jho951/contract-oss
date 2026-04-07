# 1계층 OSS

이 문서는 1계층 OSS 레포를 하나의 묶음으로 정리한다.

## 공통

- 계층: 1계층 OSS
- 기준: `oss-contract`
- 동기화 기준: 각 레포의 `sync-final/<repo>/CONTRACT_SYNC.md`
- 공통 역할: 기능 구현과 published artifact 발행

## `auth`

- 상태: 존재
- 책임: 인증 처리, principal / token / session, JWT / OAuth2 / Spring 연동
- 범위: `auth-core`, `auth-jwt`, `auth-session`, `auth-hybrid`, `auth-spring`, `auth-spring-boot-starter`, `auth-common-test`

## `ip-guard`

- 상태: 존재
- 책임: IP 허용/차단, 요청 진입 제어, core 판단 로직, Spring 연동
- 범위: `ip-guard-core`, `ip-guard-spring`, `ip-guard-spring-boot-starter`, `ip-guard-common-test`

## `rate-limiter`

- 상태: 존재
- 책임: IP / 사용자 ID / API 키 기준 rate limit, in-memory 제한, Redis 기반 분산 제한, Spring 연동
- 범위: `rate-limiter-core`, `rate-limiter-redis`, `rate-limiter-spring`, `rate-limiter-spring-boot-starter`, `rate-limiter-common-test`

## `audit-log`

- 상태: 존재
- 책임: 구조화 감사 로그
- 범위: `audit-log-api`, `audit-log-core`, `audit-log-autoconfigure`, `audit-log-spring-boot-starter`, `audit-log-common-test`

## `policy-config`

- 상태: 존재
- 책임: 정책 키 / 설정 소스 조회
- 범위: `policy-config-core`, `policy-config-spring`, `policy-config-spring-boot-starter`, `policy-config-common-test`

## `plugin-policy-engine`

- 상태: 존재
- 책임: 정책 조합 / 평가
- 범위: `plugin-policy-engine-core`, `plugin-policy-engine-spring`, `plugin-policy-engine-spring-boot-starter`, `plugin-policy-engine-common-test`

## `file-storage`

- 상태: 존재
- 책임: 파일 저장 추상화, 조회, 경로, ACL
- 범위: `file-storage-api`, `file-storage-core`, `file-storage-spring`, `file-storage-spring-boot-starter`, `file-storage-common-test`

## `notification`

- 상태: 존재
- 책임: 일반 알림 메시지 모델, 전달 채널 조합, Spring 연동
- 범위: `notification-api`, `notification-core`, `notification-spring`, `notification-spring-boot-starter`, `notification-common-test`
