# 1계층 GitHub Actions 표준

이 문서는 1계층 OSS 레포에 공통으로 적용할 GitHub Actions workflow 표준을 정의한다.

## 목적

- 테스트와 배포 절차를 통일한다.
- 태그 기반 릴리즈를 표준화한다.
- Maven Central publish 흐름을 통일한다.

## 표준 workflow

- 파일명: `publish.yml`
- 트리거: `push` on tag `v*`
- job 1: `test`
- job 2: `publish`
- publish는 test 성공 후에만 실행

## 공통 step

- `actions/checkout@v4`
- `actions/setup-java@v4`
- `gradle/actions/setup-gradle@v4`
- `./gradlew test`
- `./gradlew publish`

## 공통 secret

- `OSSRH_USERNAME`
- `OSSRH_PASSWORD`
- `SIGNING_KEY_ID`
- `SIGNING_KEY`
- `SIGNING_PASSWORD`

## 공통 규칙

- tag push시에만 publish한다.
- branch push는 publish하지 않는다.
- workflow 이름은 `publish`로 통일한다.
- test와 publish job을 분리한다.

## auth 기준 의미

- `auth`는 이 표준의 기준 workflow를 가진다.
- 나머지 1계층 OSS도 같은 구조를 따른다.
- 레포별로 job 이름이나 순서가 달라지면 안 된다.

