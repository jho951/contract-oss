# 1계층 gradle.properties 표준

`gradle.properties`는 1계층 OSS의 build, publish, SCM metadata에 필요한 공통 값을 둔다.

## 필수 key

- `release_version`
- `release_group`
- `java_version`
- `encoding`
- `github_org`
- `github_repo`
- `org.gradle.jvmargs`
- `org.gradle.parallel=true`
- `org.gradle.caching=true`
- `org.gradle.configuration-cache=true`

## dependency version key

dependency version key는 필요한 레포에만 둔다.

- `junit_version`
- `jjwt_version`
- 기타 레포별 외부 dependency version

Spring Boot 관련 key는 현재 1계층 OSS 기본 구조에 두지 않는다.
Spring Boot starter나 autoconfigure 책임은 2계층 platform에서 다룬다.

## release_version 규칙

- `release_version`은 반드시 존재한다.
- `release_version`은 배포 버전의 기준값이다.
- 릴리스 태그 publish 시 `-Prelease_version=<version>`으로 주입한다.
- 영구 fallback 값으로 릴리스 버전을 고정하지 않는다.
- tag의 `v` prefix는 workflow에서 제거해 artifact version으로 사용한다.

## release_group 규칙

- `release_group`은 Maven group 기준값이다.
- build script에서 group을 하드코딩하지 않는다.
- 모든 1계층 OSS는 같은 group 정책을 따른다.

## SCM metadata 규칙

- `github_org`와 `github_repo`를 둔다.
- POM의 `url`, `scm.connection`, `scm.developerConnection`은 이 값에서 조립한다.
- SCM URL을 `build.gradle`에 직접 하드코딩하지 않는다.

## 금지 사항

- 레포마다 다른 version key 이름 사용
- publish script에서 version 하드코딩
- release version 영구 저장
- SCM URL 하드코딩
- 사용하지 않는 dependency version key 누적

## 검증 항목

- `release_version` key가 있는가
- CI에서 `release_version` override가 가능한가
- `release_group`이 있는가
- `java_version`이 있는가
- `github_org` / `github_repo`가 있는가
- Gradle parallel / caching / configuration-cache key가 있는가

## 템플릿

```properties
release_version=
release_group=io.github.jho951
java_version=17
encoding=UTF-8

github_org=jho951
github_repo=<repo-name>

junit_version=<junit-version>

org.gradle.jvmargs=-Xmx2g -Dfile.encoding=UTF-8
org.gradle.parallel=true
org.gradle.caching=true
org.gradle.configuration-cache=true
```

필요한 레포에만 선택 key를 추가한다.

```properties
jjwt_version=<jjwt-version>
```
