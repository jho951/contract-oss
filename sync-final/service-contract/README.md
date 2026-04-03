# service-contract

`service-contract`는 실제 서비스 서버들의 계약 기준 저장소다.

## 책임

- 서비스 요청/응답 스펙
- 서비스 간 인터페이스
- 서비스별 환경변수 규격
- 서비스별 OpenAPI 규약
- 서비스별 공통 에러 코드
- 서비스 레벨 호환 규칙

## 기준

- platform과 OSS 사이의 기준은 [oss-contract](https://github.com/jho951/oss-contract)다.
- service와 platform 사이의 기준은 이 저장소다.

## 범위

- API contract
- inter-service contract
- env contract
- OpenAPI contract
- error contract
- compatibility contract

## 제외 범위

- platform 내부 구현
- OSS 내부 구현
- 서비스 구현 코드

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)

