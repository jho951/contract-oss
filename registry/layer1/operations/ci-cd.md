# 1계층 CI/CD 표준

1계층 OSS 레포는 최신 tag 기준으로 공통적으로 `build.yml`과 `publish.yml`을 가진다.

## 기본 원칙

- branch / pull request 검증은 `build.yml`에서 수행한다.
- Maven Central publish는 `publish.yml`에서 수행한다.
- publish는 tag push에서만 수행한다.
- `release_version`은 publish job에서만 주입한다.
- publish는 GitHub Actions secret 기반으로 수행한다.
- nmcp settings가 활성화된 상태에서 aggregation publish task를 실행한다.

## 권장 workflow

```text
.github/workflows/
  build.yml
  publish.yml
```

## build.yml 기준

- branch push와 pull request에서 실행한다.
- `./gradlew clean test` 또는 동등한 검증을 수행한다.
- Maven Central credential과 signing secret을 요구하지 않는다.
- 생성 산출물을 commit하지 않는다.

## publish.yml 기준

- `v*` tag push에서만 실행한다.
- tag에서 `v` prefix를 제거해 `release_version`으로 주입한다.
- publish 전에 test를 수행한다.
- `publishAggregationToCentralPortal` 또는 동등한 nmcp task를 실행한다.
- Maven Central credential과 signing secret을 env로 주입한다.

### publish.yml 구조

```yaml
on:
  push:
    tags:
      - 'v*'

jobs:
  publish:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '<java-version>'

      - uses: gradle/actions/setup-gradle@v4

      - name: Publish to Maven Central
        run: ./gradlew clean test publishAggregationToCentralPortal -Prelease_version=${GITHUB_REF_NAME#v}
        env:
          MAVEN_CENTRAL_USERNAME: ${{ secrets.MAVEN_CENTRAL_USERNAME }}
          MAVEN_CENTRAL_PASSWORD: ${{ secrets.MAVEN_CENTRAL_PASSWORD }}
          SIGNING_KEY: ${{ secrets.SIGNING_KEY }}
          SIGNING_PASSWORD: ${{ secrets.SIGNING_PASSWORD }}
```

## GitHub 운영 파일

최신 tag 기준으로 다수 레포가 아래 파일을 가진다. SOT 기준에서도 유지한다.

```text
.github/ISSUE_TEMPLATE/
.github/pull_request_template.md
```

PR 템플릿 파일명은 `.github/pull_request_template.md`로 통일한다.

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
