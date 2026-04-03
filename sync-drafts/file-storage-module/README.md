# platform-storage file-storage-module

이 저장소는 `platform-storage`의 파일 저장 추상화 구현 레포다.

## 역할

- 파일 저장 인터페이스
- 저장/조회 추상화
- 구현체 교체 가능한 구조
- storage path 규칙의 기준 제공

## 기준 문서

- 공통 계약과 경계 규칙은 [oss-contract](https://github.com/jho951/oss-contract)를 기준으로 한다.
- 실제 서비스 서버의 계약은 [service-contract](https://github.com/jho951/service-contract)를 기준으로 한다.

## 포함 범위

- 저장/조회 인터페이스
- 파일 경로 규칙
- 구현체 교체 가능한 abstraction

## 제외 범위

- 인증 책임
- 정책 엔진 책임
- 감사 로그 책임
- 서비스 비즈니스 로직

## 문서 진입점

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)

