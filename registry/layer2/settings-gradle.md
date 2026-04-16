# settings.gradle 구조 기준 - 2계층 Platform

2계층 platform의 `settings.gradle`은 platform module과 선택적 local layer1 substitution을 명확히 드러내야 한다.

## 공통 구조

```groovy
rootProject.name = '<platform-repo-name>'

include '<platform-module-1>'
include '<platform-module-2>'
```

## module 기준

- `bom`: platform 내부 모듈 버전 정렬
- `api` 또는 `spi`: 3계층이 의존할 수 있는 공개 계약
- `core`: platform orchestration 핵심
- capability adapter: 흡수한 1계층 OSS를 platform 책임으로 조립
- `autoconfigure`: Spring Boot 자동 구성
- `starter`: 3계층 소비 진입점
- `common-test` 또는 `test-support`: 테스트 지원
- sample consumer: 내부 검증용

## local layer1 substitution

`platform-governance`, `platform-resource`처럼 로컬 1계층 소스로 사전 검증하는 경우 아래 원칙을 따른다.

- `useLocalLayer1` 같은 명시적 property로만 활성화한다.
- 기본 build는 published artifact를 사용한다.
- substitution 대상은 실제 1계층 publish module과 일치해야 한다.
- local substitution은 production publish 경로가 아니다.

## 현재 module 축

- `platform-security`: security pipeline, role starter, web/autoconfigure 중심
- `platform-governance`: audit/config/engine 조립 중심
- `platform-resource`: resource api/spi/core, file-storage/notification adapter, local/jdbc/autoconfigure/starter 중심
