# platform-resource file-storage

`file-storage`는 `platform-resource`의 파일 저장 추상화 구현 레포다.

## 책임

- 파일 저장 인터페이스
- 저장/조회 추상화
- 구현체 교체 가능한 구조
- storage path 규칙의 기준 제공

## 권장 모듈

- `file-storage-api`
- `file-storage-core`
- `file-storage-spring`
- `file-storage-spring-boot-starter`
- `file-storage-common-test`

## 모듈 설명

- `file-storage-api`: 저장/조회 인터페이스
- `file-storage-core`: 파일 경로와 저장 규칙
- `file-storage-spring`: Spring 어댑터
- `file-storage-spring-boot-starter`: 소비 진입점
- `file-storage-common-test`: 테스트 지원

## 제외 범위

- 인증 책임
- 정책 엔진 책임
- 감사 로그 책임
- 서비스 비즈니스 로직

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)
5. [docs/backend-strategy.md](docs/backend-strategy.md)
