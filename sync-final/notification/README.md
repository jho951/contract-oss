# notification

`notification`은 일반 알림 추상화 OSS다.

## 책임

- 알림 메시지 모델 정의
- 알림 전달 인터페이스 제공
- 여러 전달 채널의 조합
- Spring 연동

## 권장 모듈

- `notification-api`
- `notification-core`
- `notification-console`
- `notification-email`
- `notification-webhook`
- `notification-slack`
- `notification-spring`
- `notification-spring-boot-starter`
- `notification-common-test` (test-only)

## 모듈 설명

- `notification-api`: 메시지 모델과 전달 인터페이스
- `notification-core`: 채널 조합 dispatcher와 기본 전달 구현
- `notification-console`: 콘솔 출력 채널 어댑터
- `notification-email`: SMTP 이메일 채널 어댑터
- `notification-webhook`: HTTP webhook 채널 어댑터
- `notification-slack`: Slack webhook 채널 어댑터
- `notification-spring`: Spring 자동 구성과 adapter
- `notification-spring-boot-starter`: 소비 진입점
- `notification-common-test`: 테스트 픽스처와 공용 테스트 유틸

## 제외 범위

- 인증
- 정책 평가
- 감사 저장
- 파일 저장
- 서비스 비즈니스 로직

## 버전 정책

- 기본 버전 SOT는 `gradle.properties`의 `version`이다.
- 릴리스 시에만 `releaseVersion`으로 임시 override한다.
- 태그 push 시 `releaseVersion`이 주입되어 Maven Central에 publish한다.

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)
5. [docs/delivery-model.md](docs/delivery-model.md)
6. [docs/channel-adapters.md](docs/channel-adapters.md)
7. [docs/api-model.md](docs/api-model.md)
