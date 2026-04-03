# 1계층 build.gradle 표준

이 문서는 `auth`를 기준으로 1계층 OSS 레포의 Gradle 구조를 통일하기 위한 표준이다.

## 목표

- 모든 1계층 OSS가 같은 루트/모듈 구조를 갖게 한다.
- publishing과 testing 규칙을 공통화한다.
- 멀티모듈 레포의 역할을 명확히 나눈다.

## 기준 구조

### 루트

루트 `build.gradle`은 공통 설정만 담당한다.

- Java toolchain
- 공통 repositories
- UTF-8 encoding
- 공통 test 설정
- 공통 publishing 설정 convention
- 공통 signing 설정 convention
- 서브모듈 공통 규칙

### 모듈

각 모듈 `build.gradle`은 모듈 역할만 담당한다.

- 의존성 선언
- 필요한 경우 추가 plugin
- 모듈별 테스트 보강
- 모듈별 POM 설명 보강

## 권장 루트 플러그인

- `java-library`
- `maven-publish`
- `signing`

## 권장 루트 설정

- Java 17 toolchain
- `withSourcesJar()`
- `withJavadocJar()`
- `UTF-8`
- `mavenCentral()`
- `OSSRH` publish repository
- in-memory signing

## 권장 루트 책임

- 공통 POM 메타데이터
- 공통 Maven Central 배포 convention
- 공통 release version 처리
- 서브모듈 공통 컴파일 옵션

## 권장 모듈 책임

- `auth-core` 같은 핵심 모듈
- 전략 모듈
- Spring adapter 모듈
- starter 모듈
- common-test 모듈

## 모듈별 규칙

- `*-core`는 순수 Java 라이브러리다.
- `*-spring`은 Spring 의존만 가진다.
- `*-spring-boot-starter`는 자동 설정 진입점이다.
- `*-common-test`는 테스트 전용이다.
- `*-autoconfigure`는 필요한 경우에만 둔다.

## 공통 루트 템플릿

루트 `build.gradle`은 아래 형태를 기본으로 한다.

```gradle
plugins {
    id 'java-library' apply false
    id 'maven-publish' apply false
    id 'signing' apply false
}

allprojects {
    group = 'io.github.jho951'
    version = findProperty('releaseVersion') ?: '0.1.0-SNAPSHOT'

    repositories {
        mavenCentral()
    }
}

subprojects {
    apply plugin: 'java-library'
    apply plugin: 'maven-publish'
    apply plugin: 'signing'

    java {
        toolchain {
            languageVersion = JavaLanguageVersion.of(17)
        }
        withSourcesJar()
        withJavadocJar()
    }

    tasks.withType(JavaCompile).configureEach {
        options.encoding = 'UTF-8'
    }

    publishing {
        publications {
            mavenJava(MavenPublication) {
                from components.java
            }
        }
    }

    signing {
        useInMemoryPgpKeys(
            findProperty('signingKeyId') ?: System.getenv('SIGNING_KEY_ID'),
            findProperty('signingKey') ?: System.getenv('SIGNING_KEY'),
            findProperty('signingPassword') ?: System.getenv('SIGNING_PASSWORD')
        )
        sign publishing.publications.mavenJava
    }
}
```

## 모듈 템플릿

모듈 `build.gradle`은 아래 형태를 기본으로 한다.

```gradle
dependencies {
    // module-specific dependencies only
}
```

## auth 기준 의미

- `auth-core`는 루트 공통 설정 위에서 동작한다.
- `auth-jwt`, `auth-session`, `auth-hybrid`는 루트 설정을 그대로 공유한다.
- `auth-spring`, `auth-spring-boot-starter`는 루트 설정 위에 Spring 의존만 추가한다.
- `auth-common-test`는 테스트 전용 의존성을 추가한다.

## 적용 원칙

- 루트 build는 공통 설정만 둔다.
- 모듈 build는 역할별 의존성만 둔다.
- publish 규칙은 레포 전체에서 동일하게 유지한다.
- version은 tag 기반으로 주입한다.
- POM 메타데이터는 모듈별로 보강할 수 있다.
