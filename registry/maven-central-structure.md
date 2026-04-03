# Maven Central 구조

이 문서는 1계층 OSS가 Maven Central에 올라가는 구조를 정리한다.

## 전제

- 1계층 OSS는 모두 라이브러리다.
- 공개 배포는 Maven Central을 기준으로 한다.
- 태그가 릴리즈의 기준이다.

## 공통 좌표

- `groupId`는 하나의 조직 기준으로 통일한다.
- `artifactId`는 레포 이름 또는 정해진 모듈 이름으로 통일한다.
- `version`은 release tag와 맞춘다.

## 릴리즈 규칙

- `v` prefix 여부를 한 번 정하고 일관되게 유지한다.
- breaking change는 major version으로 올린다.
- snapshot은 내부 검증용으로만 사용한다.

