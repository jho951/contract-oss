# platform-resource

## 목표 역할

- 파일과 리소스 lifecycle 플랫폼
- 저장, metadata, access, owner, kind, lifecycle 표준화

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

## 의존 방향

- `platform-resource -> platform-governance`는 가능하다.
- `platform-resource <-> platform-integrations` 순환 의존은 금지한다.
