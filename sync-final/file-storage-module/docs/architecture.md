# Architecture

`file-storage-module`은 파일 저장 기능을 추상화한다.

## 원칙

- storage abstraction은 플랫폼 책임이다.
- 서비스는 저장 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.

## 구성

- `file-storage-api`
- `file-storage-core`
- `file-storage-spring`
- `file-storage-spring-boot-starter`
- `file-storage-common-test`

