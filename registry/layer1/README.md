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

## 현재 구조에서 확인된 차이

- `notification`에는 `CONTRACT_SYNC.md`가 남아 있다.
- `policy-config`, `notification`에는 `.gradle`, `.idea`가 tag tree에 포함되어 있다.
- `audit-log`에는 `build` 디렉터리가 tag tree에 포함되어 있다.
- PR 템플릿 파일명이 `pull_request_template.md`와 `Pull_request_template.md`로 섞여 있다.
- 테스트/CI 문서명이 `testing-and-ci.md`와 `test-and-ci.md`로 섞여 있다.
- `audit-log` docs에는 대문자 문서명(`ARCHITECTURE.md`, `CONFIGURATION.md`, `RUNBOOK.md`, `TROUBLESHOOTING.md`, `USAGE.md`)이 섞여 있다.

## 제거 대상

1계층 OSS 레포에는 아래 파일과 디렉터리를 두지 않는다.

- `CONTRACT_SYNC.md`
- `.gradle/`
- `.idea/`
- `build/`
- 레포 루트의 생성 산출물
- SOT와 충돌하는 별도 계약 문서

## 책임 기준

- 1계층 OSS는 순수 기능 모듈의 본질, 규칙, 계약을 정의한다.
- 1계층 OSS는 2계층 platform이 조립할 published artifact를 제공한다.
- 1계층 OSS는 직접 consumer-facing platform이 아니다.
- Spring Boot starter, 서비스 정책, 도메인 권한 판단, platform 조립 책임은 1계층 OSS의 기본 책임이 아니다.

## 반영 기준

- 1계층 OSS 변경은 문서, build, workflow, publish 흐름을 같은 release 단위로 본다.
- 현재 구현을 SOT로 흡수할 때는 최신 tag 기준 구조를 먼저 기록한다.
- SOT 확정 후에는 각 레포를 `registry/layer1` 기준에 맞춰 정리한다.
- 한 번에 한 레포를 반영한다.
- 큰 구조 변경은 문서 변경과 build/publish 변경을 분리할 수 있다.

## 기준 문서

- [properties-standard.md](properties-standard.md): `gradle.properties` 표준
- [build-gradle.md](build-gradle.md): `build.gradle` 구조 기준
- [settings-gradle.md](settings-gradle.md): `settings.gradle` 구조 기준
- [ci-cd.md](ci-cd.md): CI/CD 표준
- [maven-central.md](maven-central.md): Maven Central publish 기준
- [repository-readme.md](repository-readme.md): README 구조 기준
- [docs-structure.md](docs-structure.md): docs 구조 기준
- [checklist.md](checklist.md): 점검표
