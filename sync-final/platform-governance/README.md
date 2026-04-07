# platform-governance

`platform-governance`는 `audit-log`, `policy-config`, `plugin-policy-engine`를 흡수하는 2계층 governance platform이다.

## 책임

- 정책 관리
- 정책 실행
- 감사 추적
- 운영 통제
- governance integration API 제공

## 권장 모듈

- `platform-governance-api`
- `platform-governance-core`
- `platform-governance-spring`
- `platform-governance-autoconfigure`
- `platform-governance-spring-boot-starter`
- `platform-governance-common-test`

## 모듈 설명

- `platform-governance-api`: 외부 노출용 governance integration API
- `platform-governance-core`: audit-log / policy-config / plugin-policy-engine 조립 핵심
- `platform-governance-spring`: Spring 어댑터
- `platform-governance-autoconfigure`: 자동 설정
- `platform-governance-spring-boot-starter`: 소비 진입점
- `platform-governance-common-test`: 공용 테스트 지원

## 제외 범위

- 인증
- 파일 저장
- 서비스 비즈니스 로직

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)
