# platform-resource

`platform-resource`는 `file-storage`와 `notification`을 흡수하는 2계층 resource platform이다.

## 책임

- 파일 저장
- 조회
- 경로 규칙
- ACL
- object / file 추상화
- 알림 메시지 전달
- 전달 채널 조합
- resource integration API 제공

## 권장 모듈

- `platform-resource-api`
- `platform-resource-core`
- `platform-resource-spring`
- `platform-resource-autoconfigure`
- `platform-resource-spring-boot-starter`
- `platform-resource-common-test`

## 모듈 설명

- `platform-resource-api`: 외부 노출 resource API
- `platform-resource-core`: file-storage / notification 조립 핵심
- `platform-resource-spring`: Spring 어댑터
- `platform-resource-autoconfigure`: 자동 설정
- `platform-resource-spring-boot-starter`: 소비 진입점
- `platform-resource-common-test`: 공용 테스트 지원

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
