# Modules

이 저장소의 모듈은 파일 저장 책임을 분리해서 담는다.

## 모듈 역할

- `file-storage-api`: 저장 인터페이스
- `file-storage-core`: 경로/조회 규칙
- `file-storage-spring`: Spring 어댑터
- `file-storage-spring-boot-starter`: 자동 설정 진입점

## 모듈 원칙

- 공통 인터페이스는 api에 둔다.
- 경로 규칙은 core에 둔다.
- Spring 종속성은 adapter와 starter로 격리한다.

