# service-contract

이 저장소는 실제 서비스 서버들의 계약 기준 저장소다.

## 역할

- 서비스 요청/응답 스펙
- 서비스 간 인터페이스
- 서비스별 환경변수 규격
- 서비스별 OpenAPI 규약
- 서비스별 공통 에러 코드
- 서비스 레벨 호환 규칙

## 기준 문서

- 플랫폼과 OSS 사이의 기준은 [oss-contract](https://github.com/jho951/oss-contract)다.
- 서비스와 플랫폼 사이의 기준은 이 저장소다.

## 포함 범위

- 서비스 API 계약
- 서비스 간 계약
- env 규격
- OpenAPI 규약
- error code
- compatibility rule

## 제외 범위

- platform-security 내부 구현
- platform-governance 내부 구현
- platform-storage 내부 구현
- 1계층 OSS 구현 세부사항

## 문서 진입점

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)

