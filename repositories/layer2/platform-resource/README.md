# platform-resource

## 목표 역할

- 파일과 리소스 lifecycle 플랫폼
- 저장, metadata, access, owner, kind, lifecycle 표준화

## 위치

- 이 문서는 현재 조직 표준 resource line으로 운영하는 `platform-resource`를 설명한다.
- 같은 1계층 OSS (`file-storage`, `notification`)를 바탕으로 다른 resource 2계층 line을 만드는 것은 가능하다.
- 아래 starter와 bridge는 `platform-resource` line의 published surface이지, 1계층을 `platform-resource`에 영구 고정한다는 뜻은 아니다.

## 현재 main 반영 포인트

- 기본 소비 진입점은 현재 `platform-resource` line에서 `platform-resource-starter`다.
- `platform-resource-filestorage-bridge-starter`는 raw `FileStorage` bean을 platform resource port로 흡수한다.
- `platform-resource-notification-bridge-starter`는 raw `NotificationDispatcher` bean을 resource lifecycle publish 경로로 흡수한다.
- sample consumer는 서비스가 storage adapter와 notification adapter를 직접 묶지 않아도 되는 경로를 검증한다.

## 주로 소비하는 OSS

- `file-storage`
- `notification`

## 플랫폼이 소유해야 할 것

- upload, download, delete 공통 흐름
- presigned URL 발급
- 파일 크기, MIME, 경로 규칙
- resource 메타데이터 모델
- owner, kind, access, lifecycle
- storage provider 추상화

## 서비스가 해야 하는 것

- resource를 도메인 엔티티에 연결
- 첨부파일, 프로필 이미지 같은 도메인 의미를 소유
- 필요한 metadata를 서비스 API와 연결

## 서비스가 하지 말아야 하는 것

- 직접 S3 SDK 호출
- 직접 파일 검증 로직 구현
- 직접 presigned URL 발급
- 서비스마다 다른 경로 규칙 사용

## 검증 기준

- resource starter와 bridge starter 두 개가 publish surface에 포함돼야 한다.
- `verifyPublishedSurface`, `verifyStarterContract`, `verifyConsumerConformance`, `verifyStage5Contract`를 기본 gate로 본다.

## 의존 방향

- `platform-resource -> platform-governance`는 가능하다.
- `platform-resource <-> platform-integrations` 순환 의존은 금지한다.
