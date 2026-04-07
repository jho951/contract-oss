# 1계층 공통 점검표

이 문서는 1계층 OSS 레포를 실제로 점검할 때 쓰는 공통 체크리스트다.

## 점검 범위

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- OSS별 추가 문서
- `gradle.properties`
- `build.gradle`
- `.github/workflows/publish.yml`

## 공통 확인 항목

- 역할 설명이 `oss-contract`와 일치하는가
- 모듈 설명이 README에 있는가
- `gradle.properties`에 `version`이 있는가
- `releaseVersion`이 릴리스 시에만 쓰이는가
- `github_org` / `github_repo`로 SCM URL을 조립하는가
- `build.gradle`이 `java-library` 기반인가
- `maven-publish`와 `signing` 구조가 있는가
- `publish.yml`이 tag 기반 publish만 수행하는가
- test / verify와 publish가 분리되어 있는가
- Maven Central metadata가 누락되지 않았는가
- platform 책임과 OSS 구현 책임이 섞이지 않았는가

## 레포별 추가 확인

- `auth`: `docs/oauth2-design.md`
- `ip-guard`: `docs/access-flow.md`
- `rate-limiter`: `docs/redis-strategy.md`
- `audit-log`: 표준 이벤트 모델 문서
- `policy-config`: 설정 소스 해석 문서
- `plugin-policy-engine`: 평가 모델 문서
- `file-storage`: 저장 전략 문서
- `notification`: delivery model, channel adapters, API model 문서

## 판정 기준

- 핵심 항목이 빠지면 동기화 미완료다.
- 구조는 맞지만 문구가 다르면 문서 보정이 필요하다.
- `gradle.properties`와 `publish.yml`이 표준과 다르면 빌드/배포 기준 미달이다.
