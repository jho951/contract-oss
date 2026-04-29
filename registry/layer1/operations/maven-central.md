# 1계층 Maven Central 구조 표준

## 목적

- `gradle.properties`, `build.gradle`, `settings.gradle`, `publish.yml`의 책임을 분리한다.
- 모든 1계층 OSS가 같은 release / publish 구조를 사용하게 한다.
- publish 가능한 artifact metadata를 통일한다.

## gradle.properties 책임

- `release_version`: publish 시 주입되는 artifact version
- `release_group`: Maven group
- `java_version`: Java toolchain 기준
- `github_org`, `github_repo`: POM SCM metadata 조립 기준

## build.gradle 책임

- `java-library`, `maven-publish`, `signing` 구조 제공
- sources jar / javadoc jar 생성
- Maven Central POM metadata 작성
- signing 설정
- module publication 정의

## settings.gradle 책임

- root project name 고정
- publish 대상 module include
- `com.gradleup.nmcp.settings` 적용
- `nmcpSettings { centralPortal { ... } }` 설정
- `publishingType = 'AUTOMATIC'` 사용

## POM metadata

모든 publication은 아래 metadata를 가진다.

- `name`
- `description`
- `url`
- `licenses`
- `scm`
- `developers`

## publish.yml 책임

- tag push에서만 publish한다.
- tag에서 `release_version`을 주입한다.
- test 후 nmcp aggregation publish task를 실행한다.
- Maven Central credential과 signing secret을 사용한다.


## 검증 항목

- `release_version`이 publish 시점에만 쓰이는가
- `github_org`와 `github_repo`로 SCM URL을 조립하는가
- `build.gradle`이 publish 가능한 artifact를 만드는가
- `settings.gradle`에 nmcp settings가 있는가
- `publishAggregationToCentralPortal` 또는 동등한 task를 사용할 수 있는가
- `publish.yml`이 tag 기반으로만 publish하는가
- Maven Central metadata가 누락되지 않았는가

## 금지 사항

- publish 좌표 하드코딩
- branch push에서 publish 수행
- secret 없이 publish 수행
- 생성 산출물을 publish source에 포함
