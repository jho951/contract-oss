# platform-resource

## 기준

- GitHub: https://github.com/jho951/platform-resource
- Version: `2.0.0`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)
- platform 표준: [../../../registry/layer2/standards/platform-resource.md](../../../registry/layer2/standards/platform-resource.md)

## 흡수 대상

- `file-storage`
- `notification`

## 책임

- 리소스 소유자
- kind
- metadata catalog
- 접근 판단
- 저장 / 삭제 생명주기 알림 orchestration
- file-storage / notification primitive 조립
- resource lifecycle event 발행과 publisher composition
- 운영 local mode 차단과 kind policy fail-fast

## 현재 모듈

- `platform-resource-bom`
- `platform-resource-api`
- `platform-resource-spi`
- `platform-resource-core`
- `platform-resource-filestorage-adapter`
- `platform-resource-notification-adapter`
- `platform-resource-jdbc`
- `platform-resource-local`
- `platform-resource-autoconfigure`
- `platform-resource-starter`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/configuration.md`
- `docs/modules.md`
- `docs/usage.md`
- `docs/when-to-use.md`
- `docs/integration-ownership.md`
- `docs/private-publish.md`
- `docs/extension-guide.md`
- `docs/quality-gates.md`
- `docs/troubleshooting.md`

## README / 문서 기준

- 공개 좌표는 실제 publish artifact와 일치해야 한다.
- 흡수 대상은 1계층 기준 버전과 충돌하지 않아야 한다.
- `무엇을 제공하나`는 `settings.gradle` include 목록과 일치해야 한다.
- 책임 경계에는 platform 조립 책임과 소비자 비즈니스 책임을 명확히 나눈다.
- docs는 platform 소비와 확장에 필요한 문서만 둔다.
- 소비자별 비즈니스 정책이나 도메인 권한 판단을 platform 책임처럼 설명하지 않는다.

## 현재 version pin

- `fileStorageVersion=2.0.0`
- `notificationApiVersion=2.0.0`
- `notificationCoreVersion=2.0.1`
- `release_version=2.0.0`

## 실무 기준

- 소비자는 `platform-resource-starter`와 resource kind 정책을 기본 진입점으로 사용한다.
- `platform-resource`는 단순 file wrapper가 아니라 owner, kind, catalog, metadata, access, delete, lifecycle event, notification orchestration이 필요한 resource runtime이다.
- resource 생성 권한은 소비자가 판단하고, resource layer는 저장 이후 kind 선언, MIME/size, catalog, lifecycle 정책을 검증한다.
- 운영에서는 `platform.resource.mode=local`, 빈 kind 정책, backing `ResourceContentStore`/`ResourceCatalog` 누락을 fail-fast 대상으로 본다.
- resource lifecycle event를 governance audit으로 남겨야 할 때만 `platform-integrations`의 `platform-resource-governance-bridge`를 추가한다.
- `platform-resource`는 `ResourceLifecycleEvent`, `ResourceLifecyclePublisher`, lifecycle publisher composition, lifecycle mode fail-fast rule을 소유한다.
- `platform-resource-governance-bridge`의 source, tests, build, publish, artifact version, release tag는 `platform-integrations`가 소유한다.
- notification은 resource lifecycle 부수효과 orchestration 범위에 한정하고, 도메인별 후속 업무 처리는 소비자 override나 별도 handler가 담당한다.
- `platform-resource`는 `platform-governance` 구현체를 직접 의존하지 않는다.

## 정리 후보

- 원격 README의 소비 예시가 `platform-resource-bom:1.0.0`으로 남아 있어 `release_version=2.0.0` 기준으로 갱신이 필요하다.
