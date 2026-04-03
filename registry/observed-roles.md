# 확인된 역할

이 문서는 각 OSS 레포의 README와 루트 구조를 확인해서 정리한 역할 메모다.

## `auth`

- 인증 처리 라이브러리
- principal / token / session 중심
- JWT, OAuth2, Spring 연동 모듈 분리

## `ip-guard`

- IP 허용/차단 라이브러리
- core와 Spring Boot 연동 분리
- 요청 진입 보안 제어

## `rate-limiter`

- 요청 속도 제한 라이브러리
- IP / 사용자 ID / API 키 기준 제한
- in-memory, Redis, Spring Boot 지원

## `audit-log`

- 구조화된 감사 로그 공통 모듈
- actor, occurredAt, clientIp, action, resource, result 중심
- Spring Boot starter 제공

## `policy-config`

- 환경변수, System Properties, .properties, Map 기반 정책 조회
- 타입 안전한 `PolicyKey<T>` 조회
- Spring Boot 자동 설정 제공

## `plugin-policy-engine`

- rollout / targeting / variant 평가용 정책 엔진
- Spring Boot 지원
- file store 기반 저장 모듈 포함

## `file-storage-module`

- 파일 저장 기능 추상화
- 저장/조회 인터페이스 중심

## `notification`

- 현재 레포는 비어 있음
- 역할은 아직 미정

