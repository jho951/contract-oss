# 1계층 버전 관리 표준

이 문서는 1계층 OSS가 Maven Central에 올라갈 때의 버전 관리 규칙을 정의한다.

## 기본 원칙

- 버전은 semantic versioning을 따른다.
- release tag는 `vX.Y.Z` 형식을 사용한다.
- Maven Central에 올라가는 버전은 tag에서 유도한다.
- 로컬 개발 기본값은 snapshot으로 둔다.

## 버전 소스

- 로컬/개발: `0.1.0-SNAPSHOT`
- 릴리즈: `v1.2.3` tag
- publish 시: `releaseVersion=1.2.3`

## 운영 규칙

- tag가 릴리즈의 단일 기준이다.
- build.gradle은 `releaseVersion` property를 우선 사용한다.
- GitHub Actions는 tag 이름에서 `v`를 제거한 값을 `releaseVersion`으로 전달한다.
- snapshot 버전은 Maven Central 릴리즈에 사용하지 않는다.

## breaking change

- major version을 올린다.
- 호환 불가 변경은 이전 버전을 유지한 채 새 major tag로 릴리즈한다.

## patch / minor

- backward compatible change는 minor 또는 patch로 릴리즈한다.
- 문서만 바뀌는 경우에도 릴리즈 기록은 남긴다.

## 검증

- tag와 artifact version이 일치하는지 확인한다.
- publish 전 test가 통과해야 한다.
- publish 후 version drift가 없는지 확인한다.

