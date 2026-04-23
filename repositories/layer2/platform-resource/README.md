# platform-resource

## 기준

- GitHub: https://github.com/jho951/platform-resource
- Version: `3.0.1`
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
- `platform-resource-adapter-filestorage`
- `platform-resource-adapter-notification`
- `platform-resource-jdbc`
- `platform-resource-jdbc-relay`
- `platform-resource-support-local`
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
- `README.md`, `docs/usage.md`, `docs/private-publish.md`, `docs/extension-guide.md`는 starter, customizer, relay 같은 실제 publish surface와 같은 release 단위로 갱신한다.
- publish 예시는 내부 구현 모듈이 아니라 실제 published artifact 좌표와 확장 경계만 사용한다.
- 소비자별 비즈니스 정책이나 도메인 권한 판단을 platform 책임처럼 설명하지 않는다.

## 현재 version pin

- `fileStorageVersion=2.0.0`
- `notificationApiVersion=2.0.0`
- `notificationCoreVersion=2.0.1`
- `release_version=3.0.1`

## 실무 기준

- 소비자는 `platform-resource-starter`와 resource kind 정책을 기본 진입점으로 사용한다.
- `platform-resource`는 단순 file wrapper가 아니라 owner, kind, catalog, metadata, access, delete, lifecycle event, notification orchestration이 필요한 resource runtime이다.
- compile classpath stage-5 기준에서 `platform-resource-starter`와 `platform-resource-autoconfigure`는 `platform-resource-core` 구현을 서비스 compile surface에 직접 새지 않는다.
- resource 생성 권한은 소비자가 판단하고, resource layer는 저장 이후 kind 선언, MIME/size, catalog, lifecycle 정책을 검증한다.
- usage/private-publish 문서는 `platform-resource-starter`, `platform-resource-jdbc-relay`, customizer 확장 경계처럼 실제 publish된 소비 표면만 예시로 든다.
- 운영에서는 `platform.resource.mode=local`, 빈 kind 정책, backing `ResourceContentStore`/`ResourceCatalog` 누락을 fail-fast 대상으로 본다.
- resource lifecycle event를 governance audit으로 남겨야 할 때만 `platform-integrations`의 `platform-resource-governance-bridge`를 추가한다.
- `platform-resource`는 `ResourceLifecycleEvent`, `ResourceLifecyclePublisher`, lifecycle publisher composition, lifecycle mode fail-fast rule을 소유한다.
- `platform-resource-governance-bridge`의 source, tests, build, publish, artifact version, release tag는 `platform-integrations`가 소유한다.
- notification은 resource lifecycle 부수효과 orchestration 범위에 한정하고, 도메인별 후속 업무 처리는 소비자 override나 별도 handler가 담당한다.
- `platform-resource`는 `platform-governance` 구현체를 직접 의존하지 않는다.
- `platform-resource-core`와 starter는 `file-storage`, `notification` 1계층 타입을 직접 노출하지 않고, adapter 모듈만 1계층과 platform port를 함께 안다.

## 반영 상태

- `OUTBOX` 운영 경로를 위한 공식 `platform-resource-jdbc-relay` 모듈이 추가됐다.
- auto-config는 resource policy, lifecycle, access를 부분 확장할 수 있는 customizer 훅을 제공한다.
- production profile 기본값은 `prod`, `production`으로 통일됐다.
- `platform-resource-spi`는 2계층 내부 port 역할을 유지하고, 1계층 storage/notification 타입은 adapter layer에만 남긴다.
- `platform-resource-jdbc-relay`는 공식 published/module surface로 유지한다.
- README, usage, private-publish 예시는 `3.0.1` 기준으로 정리됐다.
- 구현 레포 `main` push와 `v3.0.1` publish까지 완료됐다.
- `platform-resource-governance-bridge:3.0.1`는 `platform-resource 3.0.1`, `platform-governance 3.0.1`, `platform-integrations 3.0.1` release train 기준으로 publish 완료 상태다.
- `v2.0.1` publish 실패와 `v2.0.2` 재배포 경위는 과거 이력으로 [troubleshooting.md](../../../troubleshooting.md)에 남긴다.
