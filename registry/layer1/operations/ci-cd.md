# 1계층 CI/CD 표준

## 기본 원칙

- 최신 tag 기준으로 공통적으로 `build.yml`과 `publish.yml`을 가진다.
- `build.yml`에서 branch / pull request 검증을 수행합니다.
- `publish.yml`에서 Maven Central publish을 수행합니다.
- publish는 GitHub Actions secret 기반이며, tag push에서만 수행합니다.
- `release_version`은 배포 시에 주입합니다.
- nmcp(New Maven Central Publishing) settings가 활성화된 상태에서 묶어서 배포 작업을 실행합니다.

## .github

### 기준

최신 tag 기준으로 OSS 레포는 아래 파일을 가집니다.

### 종류

```text
.github/ISSUE_TEMPLATE/*
.github/pull_request_template.md
```

## 금지 사항

- branch push에서 publish 수행
- build workflow에서 signing secret 요구
- 레포별로 다른 release version 주입 방식 사용
- publish job과 일반 검증 job을 한 흐름에 섞어 운영 기준을 흐리기

## 검증 항목

- `build.yml`이 일반 검증을 담당하는가
- `publish.yml`이 tag publish만 담당하는가
- `release_version` 주입 방식이 통일되어 있는가
- secret 주입 항목이 명시되어 있는가
- PR 템플릿 파일명이 통일되어 있는가
- publish 전에 test가 실행되는가

## workflow

```text
.github/workflows/
  build.yml
  publish.yml
```

## build.yml

### 기준

- 생성 산출물을 commit하지 않는다.
- pull request에서 실행한다.
- `./gradlew clean test`를 수행한다.
- Maven Central credential과 signing secret을 요구하지 않는다.

### 구조

```yaml
name: build

on:
  pull_request:
    branches: [ main ]
    paths:
      - '**/src/**'
      - '**/*.gradle'
      - '**/*.gradle.kts'
      - 'settings.gradle'
      - 'settings.gradle.kts'
      - 'gradle.properties'
      - '**/gradle.properties'
      - 'gradle/**'
      - 'buildSrc/**'
      - 'gradlew'
      - 'gradlew.bat'
      - '.github/workflows/**'
  push:
    branches: [ main ]
    paths:
      - '**/src/**'
      - '**/*.gradle'
      - '**/*.gradle.kts'
      - 'settings.gradle'
      - 'settings.gradle.kts'
      - 'gradle.properties'
      - '**/gradle.properties'
      - 'gradle/**'
      - 'buildSrc/**'
      - 'gradlew'
      - 'gradlew.bat'
      - '.github/workflows/**'

permissions:
  contents: read

concurrency:
  group: layer1-ci-${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    timeout-minutes: 20

    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: <java_version>
      - uses: gradle/actions/setup-gradle@v4
      - run: ./gradlew clean test --no-daemon --stacktrace
```

## publish.yml

### 기준
 
- `v*` tag push에서만 실행하며, tag에서 `v` prefix를 제거해 `release_version`으로 주입한다.
- publish 전에 test를 수행한다.
- `publishAggregationToCentralPortal` 또는 동등한 nmcp task를 실행한다.
- Maven Central credential과 signing secret을 env로 주입하며, 필요한 secret는 `MAVEN_CENTRAL_USERNAME`, `MAVEN_CENTRAL_PASSWORD`, `SIGNING_KEY`, `SIGNING_PASSWORD`

### 구조

```yaml
name: publish

on:
  push:
    tags:
      - 'v*'

permissions:
  contents: read

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: <java_version>
      - uses: gradle/actions/setup-gradle@v4
      - run: ./gradlew test --no-daemon --stacktrace

  publish:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: <java_version>
      - uses: gradle/actions/setup-gradle@v4
      - run: |
          VERSION="${GITHUB_REF_NAME#v}"
          ./gradlew -Prelease_version="$VERSION" publishAggregationToCentralPortal --no-daemon --stacktrace
        env:
          MAVEN_CENTRAL_USERNAME: ${{ secrets.MAVEN_CENTRAL_USERNAME }}
          MAVEN_CENTRAL_PASSWORD: ${{ secrets.MAVEN_CENTRAL_PASSWORD }}
          MAVEN_CENTRAL_GPG_PRIVATE_KEY: ${{ secrets.MAVEN_CENTRAL_GPG_PRIVATE_KEY }}
          MAVEN_CENTRAL_GPG_PASSPHRASE: ${{ secrets.MAVEN_CENTRAL_GPG_PASSPHRASE }}
```

## gradle.properties

### 책임

- `release_version`: publish 시 주입되는 artifact version
- `release_group`: Maven group
- `java_version`: Java toolchain 기준
- `github_org`, `github_repo`: POM SCM metadata 조립 기준