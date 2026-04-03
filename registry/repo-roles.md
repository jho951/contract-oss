# 레포 역할

## `oss-contract`

- 공개 가능한 계약과 경계 규칙의 SOT
- 공통 타입, 인터페이스, 버전 규칙, 네이밍 규칙 관리
- 실제 서비스와 플랫폼이 참고하는 기준 계약 저장소
- 1계층 OSS, 2계층 platform, 3계층 service의 기준 SOT

## `platform-security`

- 인증과 요청 진입 보안 구현
- `auth`, `ip-guard`, `rate-limiter` 기반
- 실제 서비스 서버가 사용하는 2계층 플랫폼

## `platform-governance`

- 감사, 정책, 정책 엔진 구현
- `audit-log`, `policy-config`, `plugin-policy-engine` 기반
- 실제 서비스 서버가 사용하는 2계층 플랫폼

## `platform-storage`

- 파일/오브젝트 저장 구현
- `file-storage-module` 기반
- 실제 서비스 서버가 사용하는 2계층 플랫폼

## `notification`

- 현재 작성 전인 1계층 OSS
- 아직 platform 흡수 대상은 미확정

## `service-contract`

- 실제 서비스 서버들의 계약 SOT
- 주문, 예약, 정산 같은 업무 서비스가 기준으로 삼는 저장소
- `oss-contract`와는 목적이 다르며, 서비스 구현 계약을 다룬다
