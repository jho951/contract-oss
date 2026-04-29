# file-storage Standard

이 문서는 `file-storage` 1계층 OSS의 표준 책임과 경계를 고정한다.

## 역할

- 파일 저장, 조회, 삭제, 이동 primitive를 제공하는 1계층 OSS
- 저장 파일 metadata와 결과 모델을 제공하는 순수 기능 계층

## 목적

- 파일 저장, 조회, 삭제, 이동 primitive를 1계층에 둔다.
- 현재 조직 표준 resource line인 `platform-resource`가 resource lifecycle runtime에 storage primitive를 조립할 수 있게 한다.
- 같은 primitive를 바탕으로 다른 resource 2계층 line도 만들 수 있게 한다.

## 계층 원칙

- `file-storage`는 1계층 OSS다.
- `file-storage`는 content storage primitive를 제공하고 resource ownership과 lifecycle은 소유하지 않는다.
- owner, kind, catalog, access policy, lifecycle event, notification orchestration은 2계층 resource platform 책임이다.
- 특정 서비스의 첨부파일 정책이나 도메인 metadata 의미는 1계층 책임이 아니다.

## 모듈 기준

- `file-storage-api`
- `file-storage-core`

## 포함해야 할 것

- 파일 저장, 조회, 삭제, 이동 계약
- 저장 파일 metadata와 결과 모델
- 로컬 디스크 참조 구현
- 경로와 예외 유틸
- storage backend 확장 지점

## 포함하지 말아야 할 것

- resource owner, kind, catalog
- resource access policy
- soft delete lifecycle policy
- lifecycle event publisher
- notification orchestration
- governance audit bridge

## 판정 기준

- bytes나 object를 저장소에 쓰고 읽는 primitive면 `file-storage` 책임이다.
- resourceId, owner, kind, catalog, lifecycle event가 필요하면 2계층 resource platform 책임이다.
