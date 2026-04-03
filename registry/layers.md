# 계층 구조

## 1계층 OSS

1계층은 개별 OSS 구현 레포다.

- `notification` - 아직 작성 전
- `auth`
- `ip-guard`
- `rate-limiter`
- `audit-log`
- `policy-config`
- `plugin-policy-engine`
- `file-storage-module`

## 2계층 Platform

2계층은 1계층 OSS를 기반으로 조립되는 private 플랫폼 레포다.

- `platform-security`
- `platform-governance`
- `platform-storage`

## 3계층 Service

3계층은 실제 고객/업무 기능을 담는 서비스 레포다.

- `service-contract` 기준의 서버 구현들
- 주문, 예약, 정산 같은 실제 비즈니스 서비스들

## 원칙

- 1계층은 기능 단위 OSS다.
- 2계층은 공통 기반 플랫폼이다.
- 3계층은 실제 서비스다.
- 2계층끼리는 직접 구현 의존을 만들지 않는다.
- 모든 공통 계약은 `oss-contract`에서만 정의한다.
