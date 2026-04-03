# Architecture

`file-storage-module`은 파일 저장 기능을 추상화하는 플랫폼 구현 레포다.

## 설계 원칙

- storage abstraction은 플랫폼 책임이다.
- 서비스는 저장 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.
- 구체 구현은 adapter로 격리한다.

## 구성 요소

- `file-storage-api`: 저장 인터페이스
- `file-storage-core`: 경로/조회 규칙
- `file-storage-spring`: Spring 통합
- `file-storage-spring-boot-starter`: 애플리케이션 진입점

## 경계

- 파일 저장 추상화는 이 저장소의 책임이다.
- 인증은 이 저장소의 책임이 아니다.
- 정책 평가는 이 저장소의 책임이 아니다.

