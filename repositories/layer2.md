# 2계층 Platform

이 문서는 2계층 platform 레포를 정리합니다.

## 공통

- 계층: 2계층 platform
- 기준: `oss-contract`
- 소유 기준: `registry/layer2/*`
- 공통 역할: 1계층 OSS를 책임 축으로 묶어서 소비자가 쉽게 가져다 쓸 수 있는 integration API를 제공
- platform 분류는 책임 기준으로 나눈다.

## `platform-security`

- 상태: 실제 레포 생성 / 구현 진행
- 흡수 대상: `auth`, `ip-guard`, `rate-limiter`
- 책임: 요청 진입 보안, 인증, IP 제어, rate limit
- 목표: 소비자가 조립하기 좋은 security integration API 제공
- 모듈: `platform-security-core`, `platform-security-spring`, `platform-security-spring-boot-starter`, `platform-security-common-test`

## `platform-governance`

- 상태: 실제 레포 생성 / 구현 진행
- 흡수 대상: `audit-log`, `policy-config`, `plugin-policy-engine`
- 책임: 감사, 정책 설정, 정책 평가
- 목표: 소비자가 조립하기 좋은 governance integration API 제공
- 모듈: `platform-governance-core`, `platform-governance-spring`, `platform-governance-spring-boot-starter`, `platform-governance-common-test`

## `platform-resource`

- 상태: 실제 레포 생성 / 구현 진행
- 흡수 대상: `file-storage`, `notification`
- 책임: 파일 저장, 조회, 경로, ACL, 알림 메시지, 전달 채널, 자원 전달
- 목표: 소비자가 조립하기 좋은 resource integration API 제공
- 모듈: `platform-resource-core`, `platform-resource-spring`, `platform-resource-spring-boot-starter`, `platform-resource-common-test`
