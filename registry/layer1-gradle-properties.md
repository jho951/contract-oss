# 1계층 gradle.properties 표준

이 문서는 1계층 OSS 레포의 `gradle.properties` 구조를 고정한다.

## 기본 원칙

- `version`은 반드시 존재한다.
- `version`은 배포 버전의 기준값이다.
- `releaseVersion`은 릴리스 시에만 임시로 주입한다.
- 하드코딩된 release fallback은 두지 않는다.
- 각 1계층 OSS 레포는 같은 키 구조를 따른다.

## 권장 키

- `version`
- `group`
- `releaseVersion` 1회성 주입용
- `javaVersion` 또는 `sourceCompatibility`
- `artifactId`가 필요하면 명시한다
- `github_org`
- `github_repo`

## 금지 사항

- 레포마다 다른 version key 이름 사용
- publish 스크립트에서 version 하드코딩
- releaseVersion 영구 저장
- 1계층 레포별로 서로 다른 키 구조 사용
- SCM URL을 build.gradle에 하드코딩

## 검증 항목

- version key 존재 여부
- releaseVersion override 가능 여부
- CI에서 version 주입 가능 여부
- Maven publish와 충돌하지 않는지 여부
