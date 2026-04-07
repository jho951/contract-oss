# 1계층 Maven Central 구조 표준

이 문서는 1계층 OSS 레포가 Maven Central에 publish되기 위한 공통 구조를 고정한다.

## 목적

- `gradle.properties`, `build.gradle`, `publish.yml`의 역할을 분리한다.
- 모든 1계층 OSS가 같은 release/publish 구조를 사용하게 한다.
- publish 가능한 artifact 메타데이터를 통일한다.

## `gradle.properties`

- `version`은 필수다.
- `version`은 배포 기준 버전이다.
- `releaseVersion`은 릴리스 시에만 임시 주입한다.
- `group`은 필요하면 명시한다.
- `javaVersion` 또는 동등한 Java 버전 키를 둘 수 있다.
- `artifactId`는 publish 좌표가 필요한 경우 명시한다.
- `github_org`와 `github_repo`를 두고 SCM URL을 조립한다.

## `build.gradle`

- `java-library` 기반으로 작성한다.
- `maven-publish`를 사용한다.
- `signing`을 사용한다.
- `sourcesJar`와 `javadocJar`를 publish한다.
- publication 이름과 artifact naming은 레포마다 다르게 두지 않는다.
- `version`과 `group`은 `gradle.properties`를 기준으로 읽는다.
- `url`, `connection`, `developerConnection`은 `github_org`/`github_repo`에서 조립한다.

## POM 메타데이터

- `name`
- `description`
- `url`
- `licenses`
- `scm`
- `developers`

## `publish.yml`

- tag push에서만 publish한다.
- branch push는 test / verify만 수행한다.
- publish job과 test job을 분리한다.
- GitHub Actions에서 `releaseVersion`을 주입한다.
- Maven Central secret을 사용한다.
- `publish` 전에 test / verify를 실행한다.

## 필요한 secret

- Maven Central 사용자 정보
- signing key
- signing password
- repository token 또는 equivalent

## 검증 항목

- `gradle.properties`에 `version`이 있는가
- `releaseVersion`이 publish 시에만 쓰이는가
- `github_org`와 `github_repo`로 SCM URL을 조립하는가
- `build.gradle`이 publish 가능한 artifact를 만드는가
- `publish.yml`이 tag 기반으로만 publish하는가
- Maven Central metadata가 누락되지 않는가

## 금지 사항

- publish 좌표를 소스 코드에 하드코딩
- 레포마다 다른 publishing 방식 사용
- branch push에서 publish 수행
- secret 없이 publish 수행
