# Architecture

`platform-governance`는 1계층 governance OSS를 조립해 3계층이 가져다 쓰기 쉬운 integration API를 제공한다.

## 원칙

- 1계층 artifact는 exact version으로만 소비한다.
- API는 최종 프레임워크 진입점이 아니라 integration API여야 한다.
- 조립 책임은 platform에만 둔다.

## 구성

- `platform-governance-api`: 외부 노출 governance API
- `platform-governance-core`: audit-log / policy-config / plugin-policy-engine 조립
- `platform-governance-spring`: Spring 어댑터
- `platform-governance-autoconfigure`: 자동 설정
- `platform-governance-spring-boot-starter`: starter 진입점
- `platform-governance-common-test`: 테스트 지원
