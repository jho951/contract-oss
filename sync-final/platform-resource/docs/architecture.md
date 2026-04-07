# Architecture

`platform-resource`는 메시지 전달과 파일 저장을 분리하지 않고 resource / delivery API로 묶는다.

## 원칙

- 파일 저장은 resource 책임이다.
- notification은 전달 책임이다.
- integration API는 3계층이 조립하기 쉬운 형태여야 한다.

## 구성

- `platform-resource-api`: 외부 노출 resource / delivery API
- `platform-resource-core`: file-storage / notification 조립
- `platform-resource-spring`: Spring 어댑터
- `platform-resource-autoconfigure`: 자동 설정
- `platform-resource-spring-boot-starter`: starter 진입점
- `platform-resource-common-test`: 테스트 지원
