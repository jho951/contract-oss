# 1계층 OSS 기준

`registry/layer1`은 1계층 OSS 레포가 따라야 하는 공통 구조와 운영 규칙을 정의한다.
현재 기준은 각 1계층 레포의 최신 tag 구조를 먼저 흡수하고, 이후 이 레포를 SOT로 삼아 통일하는 방식이다.

## 대상

- `auth`
- `ip-guard`
- `rate-limiter`
- `audit-log`
- `policy-config`
- `plugin-policy-engine`
- `file-storage`
- `notification`

## 공통 구조

1계층 OSS는 아래 구조를 기준으로 한다.

```text
README.md
build.gradle
settings.gradle
gradle.properties
gradle/
gradlew
gradlew.bat
.github/
  ISSUE_TEMPLATE/
  pull_request_template.md
  workflows/
    build.yml
    publish.yml
docs/
<module>/
  build.gradle
```

## 정리 기준

- tag tree에는 source, docs, Gradle wrapper, GitHub 운영 파일만 둔다.
- IDE 설정, Gradle 캐시, 생성 산출물, 내부 동기화 문서는 포함하지 않는다.
- PR 템플릿 파일명은 `.github/pull_request_template.md`로 통일한다.
- 테스트/CI 문서명은 `docs/test-and-ci.md`로 통일한다.
- docs 파일명은 소문자 kebab-case로 통일한다.

## 책임 기준

- 1계층 OSS는 순수 기능 모듈의 본질, 규칙, 계약을 정의한다.
- 1계층 OSS는 2계층 platform이 조립할 published artifact를 제공한다.
- 1계층 OSS는 직접 가져다 쓰지 않습니다.
- 1계층 OSS는 Spring Boot starter, 서비스 정책, 도메인 권한 판단, platform 조립 책임을 갖지 않습니다.
- 레포별 책임 경계는 `standards/`가 소유한다.
- `repositories/layer1/<repo>/README.md`는 실제 원격 레포의 현재 상태를 기록합니다.

## 반영 기준

- 1계층 OSS 변경은 문서, build, workflow, publish 흐름을 같은 release 단위로 본다.
- 현재 구현을 SOT로 흡수할 때는 최신 tag 기준 구조를 먼저 기록한다.
- SOT 확정 후에는 각 레포를 `registry/layer1` 기준에 맞춰 정리한다.
- 한 번에 한 레포를 반영한다.
- 큰 구조 변경은 문서 변경과 build/publish 변경을 분리할 수 있다.

## 기준 문서

### structure

- [gradle-properties.md](structure/gradle-properties.md): `gradle.properties` 표준
- [build-gradle.md](structure/build-gradle.md): `build.gradle` 구조 기준
- [settings-gradle.md](structure/settings-gradle.md): `settings.gradle` 구조 기준

### operations

- [ci-cd.md](operations/ci-cd.md): CI/CD 표준
- [maven-central.md](operations/maven-central.md): Maven Central publish 기준
- [checklist.md](operations/checklist.md): 점검표

### standards

- [auth.md](standards/auth.md): `auth` 책임과 경계
- [ip-guard.md](standards/ip-guard.md): `ip-guard` 책임과 경계
- [rate-limiter.md](standards/rate-limiter.md): `rate-limiter` 책임과 경계
- [audit-log.md](standards/audit-log.md): `audit-log` 책임과 경계
- [policy-config.md](standards/policy-config.md): `policy-config` 책임과 경계
- [plugin-policy-engine.md](standards/plugin-policy-engine.md): `plugin-policy-engine` 책임과 경계
- [file-storage.md](standards/file-storage.md): `file-storage` 책임과 경계
- [notification.md](standards/notification.md): `notification` 책임과 경계
