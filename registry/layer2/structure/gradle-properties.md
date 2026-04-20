# 2계층 gradle.properties 기준

`gradle.properties`는 2계층 platform의 build, dependency pin, publish metadata에 필요한 공통 값을 둔다.

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

2계층은 1계층 OSS와 Spring platform dependency를 조립하므로 version key를 명시적으로 둔다.

- `spring_boot_version`
- `spring_dependency_management_version`
- layer1 dependency version key
- platform bridge 대상 version key
- test dependency version key

## release_version 규칙

- `release_version`은 반드시 존재한다.
- tag 또는 release input에서 publish version으로 주입한다.
- 영구 fallback 값으로 릴리스 버전을 고정하지 않는다.
- platform별 version은 `repositories/layer2/README.md`의 기준 버전과 충돌하지 않아야 한다.

## release_group 규칙

- `release_group`은 platform artifact group 기준값이다.
- build script에서 group을 하드코딩하지 않는다.
- 내부 package를 쓰더라도 group 정책은 레포 단위로 일관되게 유지한다.

## SCM metadata 규칙

- `github_org`와 `github_repo`를 둔다.
- package metadata, POM metadata, generated publication metadata는 이 값에서 조립한다.
- SCM URL을 `build.gradle`에 직접 하드코딩하지 않는다.

## 금지 사항

- dynamic version, version range, `latest.release`, `+` 사용
- platform별로 다른 version key 이름 사용
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
- 1계층 dependency version key가 exact version으로 고정되어 있는가
- Gradle parallel / caching / configuration-cache key가 있는가

## 템플릿

```properties
release_version=
release_group=io.github.jho951
java_version=17
encoding=UTF-8

github_org=jho951
github_repo=<repo-name>

spring_boot_version=<spring-boot-version>
junit_version=<junit-version>

org.gradle.jvmargs=-Xmx2g -Dfile.encoding=UTF-8
org.gradle.parallel=true
org.gradle.caching=true
org.gradle.configuration-cache=true
```

platform별 1계층 dependency version key는 필요한 레포에만 추가한다.
