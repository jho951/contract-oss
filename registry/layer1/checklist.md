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
- [ ] `docs/README.md`가 있다.
- [ ] `docs/architecture.md`가 있다.
- [ ] `docs/modules.md`가 있다.
- [ ] `docs/extension-guide.md`가 있다.
- [ ] 테스트/CI 문서는 `docs/testing-and-ci.md`로 통일되어 있다.
- [ ] 트러블슈팅 문서는 `docs/troubleshooting.md`로 통일되어 있다.
- [ ] PR 템플릿은 `.github/pull_request_template.md`로 통일되어 있다.
- [ ] 라이선스 파일은 `LICENSE`로 통일되어 있다.

## 제거 점검

- [ ] `CONTRACT_SYNC.md`가 없다.
- [ ] `.gradle/`이 없다.
- [ ] `.idea/`가 없다.
- [ ] `build/`가 없다.
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

- [ ] `auth`: API key, HMAC, OIDC, service account 모듈까지 문서에 반영되어 있다.
- [ ] `ip-guard`: `ip-guard-core`, `ip-guard-spi`만 publish 범위로 둔다.
- [ ] `rate-limiter`: `rate-limiter-core`, `rate-limiter-spi` publish 범위가 명확하다.
- [ ] `audit-log`: `audit-log-api`, `audit-log-core` publish 범위가 명확하다.
- [ ] `policy-config`: `contracts`, `core`, `builder` 책임이 분리되어 있다.
- [ ] `plugin-policy-engine`: `api`, `core`, `config` 책임이 분리되어 있다.
- [ ] `file-storage`: `api`, `core` 책임이 분리되어 있다.
- [ ] `notification`: `api`, `core` 책임이 분리되어 있다.

## 판정 기준

- 제거 대상이 남아 있으면 SOT 반영 전 정리 대상이다.
- 모듈 목록과 공개 좌표가 다르면 카탈로그와 레포 문서를 먼저 맞춘다.
- build/publish 구조가 다르면 registry 기준을 먼저 확인한다.
- 책임 경계가 충돌하면 더 좁은 1계층 책임으로 자른다.
