# platform-resource Standard

이 문서는 `platform-resource`가 L5 목표 구조에서 어떤 책임을 가져야 하는지 고정한다.

## 적용 범위

- 이 문서는 현재 조직이 운영하는 resource 2계층 line으로서의 `platform-resource` 기준을 정의한다.
- 이것이 2계층 resource platform의 유일한 형태라는 뜻은 아니다.
- 다른 팀이나 프로젝트도 같은 1계층 OSS (`file-storage`, `notification`)를 사용해 다른 resource 2계층 line을 만들 수 있다.
- 다만 서비스는 raw OSS 대신 자신이 선택한 resource platform line의 contract를 소비해야 한다.

## 역할

- 파일과 리소스 lifecycle 플랫폼
- 저장, metadata, access, owner, kind, lifecycle을 표준화하는 계층

## 목적

- 서비스마다 파일 업로드와 storage 접근을 따로 만들지 않게 한다.
- 단순 file wrapper가 아니라 리소스 lifecycle 전체를 현재 조직 표준 방식으로 제공한다.
- 서비스는 도메인과 resource 연결만 하고, 저장 흐름과 정책은 platform이 가져가게 한다.

## 소유해야 할 것

- upload, download, delete 공통 흐름
- presigned URL 발급
- 파일 크기, MIME, 경로 규칙
- resource 메타데이터 모델
- owner, kind, access, lifecycle
- storage provider 추상화

## 1계층 조립 기준

- `file-storage`
- `notification`

## 포함해야 할 것

- platform-owned resource API와 SPI
- metadata catalog
- access evaluation 진입점
- lifecycle event
- local mode와 운영 mode 구분
- typed properties

## 현재 main 기준 bridge surface

- `platform-resource-starter`를 현재 `platform-resource` line의 기본 진입점으로 둔다.
- `platform-resource-filestorage-bridge-starter`는 raw `FileStorage` bean을 `ResourceContentStore` 계열 platform port로 연결하는 공식 bridge다.
- `platform-resource-notification-bridge-starter`는 raw `NotificationDispatcher` bean을 `ResourceLifecyclePublisher` 계열 platform port로 연결하는 공식 bridge다.
- 서비스는 bridge starter를 먼저 쓰고, 같은 조립을 서비스 내부에서 다시 만들지 않는다.

## 포함하지 말아야 할 것

- 단순 파일 유틸 정도로 축소된 API
- 서비스별 문서 도메인 규칙
- 서비스별 block 규칙
- 서비스별 profile 의미
- 직접 S3 SDK를 쓰는 서비스 코드

## 확장 규칙

- 서비스는 raw `file-storage` 타입을 직접 import하지 않는다.
- notification은 resource lifecycle 이후 부수효과 orchestration 범위에만 둔다.
- 리소스 접근과 lifecycle 기준은 platform이 소유하고, 도메인 의미는 서비스가 소유한다.

## 검증 기준

- `verifyPublishedSurface`는 resource starter와 sanctioned bridge starter가 publish surface에 포함되는지 확인해야 한다.
- `verifyStarterContract`는 resource starter만으로 lifecycle 기본 조립이 되는지 확인해야 한다.
- `verifyConsumerConformance`는 sample consumer가 raw storage/notification adapter를 서비스에서 직접 묶지 않아도 되는지 확인해야 한다.
- `verifyStage5Contract`는 public surface에 `FileStorage`, `NotificationDispatcher` 같은 1계층 타입이 새지 않았는지 확인해야 한다.

## 운영 프로필 기준

- production profile 기본값은 `["prod", "production"]`를 사용한다.
- `platform.resource.mode=local`, 빈 kind 정책, backing store 누락은 fail-fast 대상이다.
