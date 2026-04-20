# build.gradle 구조

> Maven Central publish 가능한 Java library 구조를 기준으로 합니다.

## 공통

### plugin

```groovy
plugins {
    id 'java-library'
    id 'maven-publish'
    id 'signing'
}
```

### 값

```groovy
group = findProperty('release_group')
version = findProperty('release_version')
```

### Java 설정

```groovy
java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(findProperty('java_version') as int)
    }
    withSourcesJar()
    withJavadocJar()
}
```

## 기준

### publication
- 모든 publish 대상 artifact는 Maven Central metadata를 가진다.
- POM에는 name, description, url, license, developer, scm 정보를 채운다.
- SCM 정보는 `github_org`, `github_repo`에서 조립한다.
- 루트 publication을 두는 경우 실제 공개 좌표와 README를 일치시킨다.
- 하위 모듈 publication은 `settings.gradle` include 목록과 일치해야 한다.

### signing 

- signing은 publish task가 실행될 때만 필요하다.
- signing key와 password는 CI secret에서 주입한다.
- secret 없이 일반 build/test가 깨지면 안 된다.

### 금지

- version, group, SCM URL 하드코딩
- 레포별로 다른 publish metadata 구조 만들기
- branch CI에서 signing secret 요구하기
- 생성 산출물을 publish source에 포함하기
