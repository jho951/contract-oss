# platform-resource Standard

이 문서는 `platform-resource`가 L5 목표 구조에서 어떤 책임을 가져야 하는지 고정한다.

## 역할

- 파일과 리소스 lifecycle 플랫폼
- 저장, metadata, access, owner, kind, lifecycle을 표준화하는 계층

## 목적

- 서비스마다 파일 업로드와 storage 접근을 따로 만들지 않게 한다.
- 단순 file wrapper가 아니라 리소스 lifecycle 전체를 공통화한다.
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

## 운영 프로필 기준

- production profile 기본값은 `["prod", "production"]`를 사용한다.
- `platform.resource.mode=local`, 빈 kind 정책, backing store 누락은 fail-fast 대상이다.
