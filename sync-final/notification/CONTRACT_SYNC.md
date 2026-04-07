# CONTRACT_SYNC - notification

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `notification`

## 버전 규칙

- 기본 버전 SOT는 `gradle.properties`의 `version`이다.
- `releaseVersion`은 릴리스 시에만 임시 override로 사용한다.
- `build.gradle`의 하드코딩 fallback은 두지 않는다.

## 확인된 역할

- 일반 알림 추상화 OSS
- 메시지 발행 / 전달 인터페이스 제공
- Spring 연동 가능
- `console` / `webhook` 채널 어댑터 제공
- `email` / `slack` 채널 어댑터 제공

## 반영 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/delivery-model.md`
- `docs/channel-adapters.md`
- `docs/api-model.md`
- `gradle.properties`
- `build.gradle`
- `settings.gradle`
- `.github/workflows/publish.yml`
