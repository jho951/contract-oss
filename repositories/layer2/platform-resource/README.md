# platform-resource

## 기준

- GitHub: https://github.com/jho951/platform-resource
- Version: `2.0.0`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)

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
- `docs/private-publish.md`
- `docs/extension-guide.md`
- `docs/quality-gates.md`
- `docs/troubleshooting.md`

## 실무 기준

- 소비자는 `platform-resource-starter`와 resource kind 정책을 기본 진입점으로 사용한다.
- `platform-resource`는 단순 file wrapper가 아니라 owner, kind, catalog, access, delete, lifecycle event가 필요한 resource runtime이다.
- resource 생성 권한은 소비자가 판단하고, resource layer는 저장 이후 kind 선언, MIME/size, catalog, lifecycle 정책을 검증한다.
- 운영에서는 `platform.resource.mode=local`, 빈 kind 정책, backing `ResourceContentStore`/`ResourceCatalog` 누락을 fail-fast 대상으로 본다.
- resource lifecycle event를 governance audit으로 남겨야 할 때만 `platform-integrations`의 `platform-resource-governance-bridge`를 추가한다.
- `platform-resource`는 `ResourceLifecycleEvent`, `ResourceLifecyclePublisher`, lifecycle publisher composition, lifecycle mode fail-fast rule을 소유한다.
- `platform-resource-governance-bridge`의 source, tests, build, publish, artifact version, release tag는 `platform-integrations`가 소유한다.
