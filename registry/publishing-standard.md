# 1계층 OSS 배포 표준

이 문서는 1계층 OSS 레포들이 Maven Central에 올라가는 공통 배포 표준을 정의한다.

## 전제

- 1계층 레포는 모두 OSS 모듈이다.
- 배포 대상은 Maven Central이다.
- 각 레포는 개별 구현이지만, 배포 방식과 메타데이터는 통일한다.
- 배포는 GitHub Actions와 태그 기반 릴리즈를 사용한다.

## 표준 원칙

- 모든 1계층 OSS는 라이브러리로 배포한다.
- 공통 좌표 규칙을 사용한다.
- 버전은 `registry/versioning-standard.md`를 따른다.
- CI/CD는 레포별로 달라도 표준 workflow 구조는 통일한다.

## 포함 항목

- `groupId`
- `artifactId`
- `version`
- `license`
- `scm`
- `developers`
- `sources jar`
- `javadoc jar`
- `signing`
- `maven publish`

## version 주입

- publish 시 `releaseVersion` property를 사용한다.
- `releaseVersion`은 tag에서 유도한다.
- local default는 snapshot이다.

## 제외 항목

- 서비스 배포
- 운영 인프라 배포
- 플랫폼 런타임 배포
