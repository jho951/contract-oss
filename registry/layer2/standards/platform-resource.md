# platform-resource Standard

이 문서는 `platform-resource` 2계층 platform의 표준 구조와 경계를 고정한다.

## 목적

- `file-storage`, `notification` 1계층 OSS를 조립하는 표준 2계층을 정의한다.
- 단순 파일 저장 wrapper가 아니라 resource owner, kind, metadata, lifecycle, event, notification orchestration을 묶는 runtime platform을 제공한다.
- 파일/리소스 책임이 있는 서비스가 저장소와 후속 알림 primitive를 직접 조립하지 않게 한다.

## 계층 원칙

- `platform-resource`는 서비스가 직접 소비하는 runtime platform이다.
- resource 생성 권한과 업무 소유권 판단은 소비자 서비스가 소유한다.
- resource layer는 저장 이후 kind 선언, MIME/size, catalog, lifecycle 정책, resource access 정책을 검증한다.
- lifecycle event 발행과 publisher composition은 `platform-resource` 본체 책임이다.
- lifecycle event를 governance audit으로 기록하는 bridge 구현은 `platform-integrations` 책임이다.
- `platform-resource`는 `platform-governance` 구현체를 직접 의존하지 않는다.

## 1계층 조립 기준

- `file-storage`: content store primitive, backend adapter, object storage operation
- `notification`: resource lifecycle 이후 알림 primitive, channel adapter, delivery model

## 포함해야 할 것

- resource owner/kind abstraction
- metadata catalog
- resource access 정책 경계
- 저장/삭제 lifecycle
- `ResourceLifecycleEvent`
- `ResourceLifecyclePublisher`
- lifecycle publisher composition
- file-storage adapter 조립
- notification adapter 조립
- local mode 차단과 kind policy fail-fast

## 포함하지 말아야 할 것

- 단순 file-storage wrapper로 축소된 API
- 소비자별 도메인 후속 업무 처리
- resource 생성 권한의 최종 판단
- governance audit 기록 구현
- security authentication/filter 조립
- 특정 서비스 전용 resource kind 하드코딩
- 특정 storage vendor 전용 정책을 platform core에 고정

## 확장 규칙

- 소비자는 `platform-resource-starter`와 resource kind 정책을 기본 진입점으로 사용한다.
- storage backend 차이는 `ResourceContentStore` 구현이나 adapter로 흡수한다.
- catalog backend 차이는 `ResourceCatalog` 구현으로 흡수한다.
- notification은 lifecycle 부수효과 orchestration에 한정하고, 도메인별 업무 처리는 소비자 override나 별도 handler가 담당한다.
- governance audit 연결이 필요하면 `platform-integrations`의 `platform-resource-governance-bridge`를 추가한다.

## 운영 기준

- 운영에서는 `platform.resource.mode=local`, 빈 kind 정책, backing `ResourceContentStore`/`ResourceCatalog` 누락을 fail-fast 대상으로 본다.
- `platform-resource-governance-bridge`의 source, tests, build, publish, artifact version, release tag는 `platform-integrations`가 소유한다.
- `platform-resource`는 bridge artifact version을 소유하지 않는다.
