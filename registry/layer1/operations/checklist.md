# 1계층 공통 점검표

이 문서는 최신 tag 기준 구현을 SOT로 흡수하거나, SOT 기준을 각 1계층 레포에 반영할 때 쓰는 체크리스트다.

## 구조 점검

- [ ] `README.md`가 있다.
- [ ] `build.gradle`이 있다.
- [ ] `settings.gradle`이 있다.
- [ ] `gradle.properties`가 있다.
- [ ] `gradle/`, `gradlew`, `gradlew.bat`이 있다.
- [ ] `.github/workflows/build.yml`이 있다.
- [ ] `.github/workflows/publish.yml`이 있다.
- [ ] `docs/readme.md`가 있다.
- [ ] `docs/architecture.md`가 있다.
- [ ] `docs/modules.md`가 있다.
- [ ] `docs/extension-guide.md`가 있다.
- [ ] docs 파일명은 소문자 `kebab-case`를 사용한다.
- [ ] 테스트/CI 문서는 `docs/test-and-ci.md`로 통일되어 있다.
- [ ] 트러블슈팅 문서는 `docs/troubleshooting.md`로 통일되어 있다.
- [ ] 대문자 docs 파일명이 없다.
- [ ] `docs/implementation-guide.md`는 레포 책임에 필요한 경우에만 둔다.
- [ ] 레포별 특화 문서는 해당 OSS 표준의 책임 범위 안에 있다.
- [ ] PR 템플릿은 `.github/pull_request_template.md`로 통일되어 있다.
- [ ] 라이선스 파일은 `LICENSE`로 통일되어 있다.

## 제거 점검

- [ ] 내부 계약 동기화 문서가 없다.
- [ ] Gradle 캐시 디렉터리가 없다.
- [ ] IDE 설정 디렉터리가 없다.
- [ ] 생성 산출물 디렉터리가 없다.
- [ ] 레포 루트에 생성 산출물이 없다.
- [ ] SOT와 충돌하는 별도 계약 문서가 없다.

## 모듈 점검

- [ ] `settings.gradle`의 include 목록이 실제 publish 대상과 일치한다.
- [ ] 각 publish 대상 모듈에 `build.gradle`이 있다.
- [ ] README의 공개 좌표가 `settings.gradle`의 모듈 목록과 일치한다.
- [ ] `docs/modules.md`가 README의 공개 좌표와 일치한다.
- [ ] Spring/starter/platform 모듈이 1계층 OSS에 섞여 있지 않다.

## build / publish 점검

- [ ] `gradle.properties`에 `release_version`이 있다.
- [ ] `release_version`은 릴리스 시점에만 주입된다.
- [ ] `release_group`이 있다.
- [ ] `java_version`이 있다.
- [ ] `github_org` / `github_repo`로 SCM URL을 조립한다.
- [ ] `build.gradle`은 `java-library`, `maven-publish`, `signing` 구조를 가진다.
- [ ] Maven Central POM metadata가 누락되지 않았다.
- [ ] `settings.gradle`에 `com.gradleup.nmcp.settings`와 `nmcpSettings { centralPortal { ... } }`가 있다.
- [ ] `publishAggregationToCentralPortal` 또는 동등한 nmcp aggregation task를 사용할 수 있다.
- [ ] `.github/workflows/publish.yml`은 tag push에서만 publish한다.
- [ ] `.github/workflows/build.yml`은 branch / PR 검증을 담당한다.
- [ ] publish job은 Maven Central credential과 signing secret을 명시한다.

## 책임 점검

- [ ] 레포 책임이 `repositories/layer1/README.md`의 책임과 일치한다.
- [ ] 레포 범위가 `repositories/layer1/README.md`의 모듈 범위와 일치한다.
- [ ] 1계층 OSS 책임과 2계층 platform 책임이 섞이지 않는다.
- [ ] 서비스 비즈니스 로직, 도메인 권한 판단, platform 조립 책임이 없다.

## 레포별 특화 점검

- [ ] `auth`는 [auth.md](../standards/auth.md)를 따른다.
- [ ] `ip-guard`는 [ip-guard.md](../standards/ip-guard.md)를 따른다.
- [ ] `rate-limiter`는 [rate-limiter.md](../standards/rate-limiter.md)를 따른다.
- [ ] `audit-log`는 [audit-log.md](../standards/audit-log.md)를 따른다.
- [ ] `policy-config`는 [policy-config.md](../standards/policy-config.md)를 따른다.
- [ ] `plugin-policy-engine`은 [plugin-policy-engine.md](../standards/plugin-policy-engine.md)를 따른다.
- [ ] `file-storage`는 [file-storage.md](../standards/file-storage.md)를 따른다.
- [ ] `notification`은 [notification.md](../standards/notification.md)를 따른다.

## 판정 기준

- 제거 대상이 남아 있으면 SOT 반영 전 정리 대상이다.
- 모듈 목록과 공개 좌표가 다르면 카탈로그와 레포 문서를 먼저 맞춘다.
- build/publish 구조가 다르면 registry 기준을 먼저 확인한다.
- 책임 경계가 충돌하면 더 좁은 1계층 책임으로 자른다.
