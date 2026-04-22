# OSS / Platform Troubleshooting

이 문서는 2026-04-22 기준으로 1계층 OSS와 2계층 platform 경계를 맞추는 과정에서 실제로 확인한 문제, 변경 이유, 수정 내역, 현재 상태를 정리한 기록이다.

이번 턴에서 새로 확인한 내용뿐 아니라, 이전 작업에서 남겨두지 못했던 release/publish 이력과 실패 원인도 함께 적는다.

## 대상 레포

- `oss-contract`
- `platform-security`
- `platform-resource`
- `platform-governance`
- `platform-integrations`

## 이번 작업의 목표

- `platform-security`에서 raw OSS SPI 직접 노출을 줄이고 platform-owned 계약으로 정리한다.
- `platform-resource`, `platform-governance`, `platform-integrations` 문서를 실제 published surface와 구현 기준에 맞춘다.
- 4개 구현 repo와 `oss-contract`의 표준/README/usage/private-publish/workflow 설명을 다시 맞춘다.

## 먼저 확인한 문제

### 1. 계약 문서와 구현 저장소 문서가 같이 움직이지 않았다

- `oss-contract`에는 새 기준이 먼저 들어가고, 실제 구현 repo 문서는 예전 표면을 설명하는 경우가 있었다.
- 특히 README, quickstart, usage, private-publish 예시가 실제 `release_version`, 현재 모듈 목록, bridge ownership, publish workflow와 어긋나 있었다.

### 2. `platform-security`가 여전히 raw OSS 타입을 public contract처럼 끌고 있었다

- `platform-security-auth` 공개 시그니처 일부가 `com.auth.*`에 직접 기대고 있었다.
- rate-limit policy 설명과 일부 확장 문구가 raw `RateLimiter`를 사실상 public surface처럼 다루고 있었다.
- auto-configuration auth wiring도 raw auth bean graph 설명과 너무 가까웠다.

### 3. runtime platform의 production profile 기준이 문서마다 달랐다

- `platform-security`, `platform-resource`, `platform-governance` 문서 중 일부는 기본 운영 profile을 `prod`만으로 설명했다.
- 실제 구현 properties 기본값은 `prod`, `production` 둘 다 포함하는 곳이 있었다.

### 4. bridge / publish ownership 설명이 드리프트했다

- `platform-resource` 문서에는 `platform-resource-governance-bridge` 예시 버전이 예전 값으로 남아 있었다.
- `platform-integrations`는 자체 publish는 맞았지만, dependency read token 설명이 build 기준만큼 명확하지 않았다.

## 판단 기준

### 1. SoT는 각 repo의 현재 build 설정과 published pin이다

- 버전 예시는 `gradle.properties`의 현재 값 기준으로 맞춘다.
- publish 문구는 실제 `.github/workflows/publish.yml`과 `build.gradle` parameter 이름 기준으로 맞춘다.
- 1계층 최신 `main`보다 2계층 platform이 실제 pin한 published version을 우선한다.

### 2. platform public surface는 platform-owned 계약으로 정리한다

- 소비 서비스가 raw OSS 타입을 직접 맞춰야 성립하는 구조는 문서/계약 모두에서 밀어낸다.
- raw OSS는 platform 내부 adapter/helper 계층에서만 흡수한다.

### 3. bridge는 본체 platform이 아니라 `platform-integrations`가 소유한다

- source platform은 event/publisher 계약만 소유한다.
- governance audit으로 변환하는 bridge source/build/publish/version/release tag는 `platform-integrations`가 소유한다.

## 과거 기록에서 복원한 이력

### 1. `platform-security`의 이전 릴리스 정리

- `platform-security`는 이번 `2.1.0` 정리 이전에 raw OSS 직접 노출 완화와 hybrid adapter 반영 작업을 거쳐 `v2.0.4`, `v2.0.5` 단계까지 올라간 상태였다.
- 과거 메모 기준 주요 변경 포인트는 다음이었다.
  - 1계층 OSS 직접 결합을 platform 소유 port/adapter 뒤로 이동
  - preset-aware production fail-fast 조정
  - gateway용 `platform-security-hybrid-web-adapter` 경로 도입
  - production profile 기본값을 `prod`, `production`으로 정리
- 과거 기록에는 다음 항목이 남아 있었다.
  - commit: `3c3848c`
  - message: `Add platform-owned security ports and hybrid adapter`
  - pushed tag: `v2.0.4`
- 이후 `platform-integrations 1.0.3`이 `securityVersion=2.0.5` 기준으로 검증되면서 실질 소비 기준은 `platform-security 2.0.5`로 정리됐다.

### 2. `platform-resource` publish 실패와 복구 이력

- `platform-resource`는 이전에 customizer 확장 포인트와 optional JDBC outbox relay를 추가하며 먼저 `v2.0.1`을 시도했다.
- 당시 기록에 남은 정보:
  - commit: `0eda434`
  - message: `Add resource customizers and jdbc outbox relay`
  - pushed tag: `v2.0.1`
- `v2.0.1` publish 실패는 코드 문제가 아니라 workflow secret 설정 문제였다.
  - workflow run id: `24737075146`
  - workflow: `publish`
  - ref: `v2.0.1`
  - conclusion: `failure`
  - 실패 step: `Validate GH_TOKEN secret`
  - 원인: `.github/workflows/publish.yml`이 `secrets.GH_TOKEN`을 강제했는데 저장소에 해당 secret이 없었다.
- 이후 조치:
  - `permissions.packages: write` 추가
  - `secrets.GH_TOKEN` 제거
  - `secrets.GITHUB_TOKEN` 사용으로 전환
  - 재배포를 위해 버전을 `2.0.2`로 상향
- 과거 기록에 남은 수정 커밋:
  - commit: `7a4171a`
  - message: `Fix publish workflow to use GitHub token`
- 재배포 결과:
  - pushed tag: `v2.0.2`
  - publish workflow run id: `24738445044`
  - conclusion: `success`
- 이번 턴에서는 그 상태 위에서 문서를 published surface 기준으로 다시 정렬했다.

### 3. `platform-integrations`의 기존 publish 상태

- 과거 기록 기준 `platform-integrations`는 이미 `1.0.3` 기준으로 두 bridge artifact publish를 마친 상태였다.
- 당시 정리된 핵심은 다음이었다.
  - `platform-security-governance-bridge`와 `platform-resource-governance-bridge` 모두 `1.0.3`
  - `platform-security 2.0.5`, `platform-governance 2.0.2`, `platform-resource 2.0.2` exact pin 기준으로 정합성 확인
  - bridge artifact publish ownership은 `platform-integrations`에 고정

### 4. `platform-governance`의 SoT 정리 이유

- 과거부터 문제였던 지점은 1계층 OSS 최신 `main`과 2계층 published pin을 혼동하기 쉬웠다는 것이다.
- `platform-governance 2.0.2` 기준으로 정리된 published pin은 아래였다.
  - `auditLogVersion=2.0.0`
  - `policyConfigVersion=2.0.0`
  - `pluginPolicyEngineVersion=2.0.1`
- 이 기준을 SoT로 삼는 이유:
  - governance 정합성 판단은 1계층 최신 소스가 아니라, 실제 published platform이 소비하는 exact version 기준이어야 한다.

### 5. 공통 troubleshooting 축

- 이전 기록에서 반복해서 드러난 문제는 아래 여섯 가지였다.
  - platform이 1계층 OSS 타입을 직접 요구하는 문제
  - runtime platform의 production profile/fail-fast 기준이 서로 달랐던 문제
  - published artifact와 문서 surface가 어긋난 문제
  - governance 연계 SPI를 잘못 해석하기 쉬운 문제
  - 2계층 SoT와 1계층 최신 `main`을 혼동하는 문제
  - publish 실패가 코드 문제인지 workflow 문제인지 분리되지 않던 문제
- 이번 턴의 수정은 이 여섯 축을 다시 현재 구현 기준으로 닫는 작업이었다.

## 실제 변경

## 1. `platform-security`

### 코드 변경

- `platform-security-auth`에 platform-owned auth 타입 추가
  - `PlatformAuthenticatedPrincipal`
  - `PlatformOAuth2UserIdentity`
  - `AuthPrincipalAdapters`
  - `PlatformSessionSupportFactory`
  - `DefaultPlatformSessionSupportFactory`
- 공개 auth 계약이 위 platform-owned 타입을 기준으로 동작하도록 정리
- 제거 전까지 공개 노출이 남는 `com.auth.*` 의존성은 `api` 범위로 승격
- `PlatformSecurityAutoConfiguration` auth wiring을 platform-owned factory 기준으로 추상화
- `PlatformRateLimitAdapter`가 raw `RateLimiter`를 직접 노출하지 않도록 변경
  - `PlatformRateLimitRequest`
  - `PlatformRateLimitDecision`
  - `PlatformRateLimitKeyType`
- policy와 facade가 platform-owned rate-limit 계약만 보도록 수정
- `platform-security-hybrid-web-adapter`에 공식 gateway 통합 표면 추가
  - `PlatformSecurityGatewayIntegration`
  - auto-configuration package 정리

### 문서 변경

- `README.md`
- `docs/architecture.md`
- `docs/configuration.md`
- `docs/extension-guide.md`
- `docs/modules.md`
- `docs/private-publish.md`
- `docs/quickstart.md`
- `docs/release-notes.md`
- `docs/troubleshooting.md`
- `docs/why-use-platform-security.md`

### 버전 변경

- `release_version=2.1.0`
- 문서 예시도 `platform-security-bom:2.1.0` 기준으로 갱신

### 로컬 커밋 상태

- commit: `34178b8`
- message: `align platform-owned security contracts and release 2.1.0`
- pushed branch: `main`
- pushed tag: `v2.1.0`
- publish workflow run id: `24762971913`
- publish conclusion: `success`

### 이전 상태와의 연결

- 이번 `2.1.0`은 `2.0.5`까지 쌓인 platform-owned contract 정리 작업을 한 번 더 밀어붙인 결과다.
- 따라서 release note에는 단순 문서 정리보다 public contract, rate-limit contract, hybrid gateway surface 변경을 모두 명시했다.

## 2. `platform-resource`

### 문서 변경

- `README.md`
- `docs/usage.md`
- `docs/private-publish.md`
- `docs/configuration.md`
- `docs/troubleshooting.md`
- `docs/integration-ownership.md`

### 반영한 내용

- `platform-resource-jdbc-relay`를 공식 published/module surface에 반영
- private publish 문서를 실제 workflow 기준인 `GITHUB_TOKEN` 흐름으로 정리
- publish/version/tag 예시를 현재 `2.0.2` 기준으로 수정
- `platform-resource-governance-bridge` 및 governance BOM 예시 버전을 현재 값으로 정리
- production profile 기본값 설명을 실제 구현 기준인 `prod`, `production`으로 맞춤

### 로컬 커밋 상태

- commit: `2ade63a`
- message: `sync resource docs with published surface`

### 이전 상태와의 연결

- 이 문서 정리는 `v2.0.2` publish 성공 이후에도 남아 있던 module list / publish guide / governance bridge example drift를 닫는 후속 작업이다.

## 3. `platform-governance`

### 확인 결과

- `README`, docs, `settings.gradle`, `gradle.properties`, workflow 기준을 전수 확인했다.
- 현재 표준 대비 큰 불일치는 찾지 못했다.
- 특히 아래 기준은 구현과 문서가 일치했다.
  - production profile 기본값 `prod`, `production`
  - `platform.governance.feature-flags.*` 우선, legacy `plugin-policy-engine.*`는 deprecated alias
  - 서비스 공식 감사 출력 SPI는 `AuditSink`
  - `AuditLogRecorder` fan-out은 compat 경로로만 허용

### 코드/문서 변경

- 없음

### 이전 상태와의 연결

- governance는 이번 턴에 수정은 없었지만, exact pin과 feature-flag prefix, `AuditSink` / `AuditLogRecorder` 경계가 이미 정리된 상태였기 때문에 기준 repo 역할을 했다.

## 4. `platform-integrations`

### 문서 변경

- `README.md`

### 반영한 내용

- bridge artifact 설명은 이미 표준과 맞아 있었다.
- 다만 실제 build 기준상 private dependency package를 읽기 위한 token 흐름이 필요해서 README에 dependency read token 설명을 추가했다.
- publish 예시가 `githubDependencyPackagesToken` / `GITHUB_READ_TOKEN` fallback 구조를 이해할 수 있게 보강했다.

### 로컬 커밋 상태

- commit: `ffcbba2`
- message: `document integration publish dependency tokens`

### 이전 상태와의 연결

- bridge artifact 자체는 이미 `1.0.3` publish 완료 상태였고, 이번 수정은 README가 실제 build/token fallback 구조를 충분히 설명하지 못하던 부분을 메운 것이다.

## 5. `oss-contract`

### 이미 반영한 계약 변경

- `registry/layer2/standards/platform-security.md`
- `registry/layer2/standards/platform-resource.md`
- `registry/layer2/standards/platform-governance.md`
- `registry/layer2/operations/publish.md`
- `repositories/layer2/platform-security/README.md`
- `repositories/layer2/platform-resource/README.md`
- `repositories/layer2/platform-governance/README.md`
- `repositories/layer2/platform-integrations/README.md`

### 추가 인덱스 변경

- `README.md`
- `registry/layer2/README.md`
- `repositories/layer2/README.md`

### 로컬 커밋 상태

- commit: `677936c`
- message: `align layer2 platform contracts with implementation repos`
- commit: `91f3012`
- message: `refresh layer2 contract indexes`

## 검증

### `platform-security`

성공:

```bash
./gradlew :platform-security-auth:test :platform-security-autoconfigure:test :platform-security-hybrid-web-adapter:test
./gradlew test
```

### `platform-resource`

성공:

```bash
./gradlew test
```

### `platform-governance`

성공:

```bash
./gradlew test
```

### `platform-integrations`

성공:

```bash
./gradlew test
```

## 과거 검증 / 배포 기록에서 중요했던 항목

- `platform-security`
  - `./gradlew :platform-security-auth:test :platform-security-autoconfigure:test :platform-security-hybrid-web-adapter:test`
  - 이후 `2.0.5` 소비 기준에서 bridge compile/test까지 통과
- `platform-resource`
  - `./gradlew clean test publishToMavenLocal -Prelease_version=2.0.2`
  - `v2.0.1`은 workflow secret 문제로 실패, `v2.0.2`는 성공
- `platform-integrations`
  - bridge 두 개 모두 `1.0.3` 기준 test/publish 완료 기록 존재

## 지금 시점의 정합 상태

- `platform-security`
  - 코드/문서/버전 정리 완료
  - `2.1.0` release 완료
- `platform-resource`
  - 문서 정합화 완료
- `platform-governance`
  - 전수 확인 결과 추가 수정 불필요
- `platform-integrations`
  - 문서 정합화 완료
- `oss-contract`
  - layer2 표준/상태 문서 정합화 완료

## push / publish 관점 현재 상태

- `platform-security`
  - `main` push 완료
  - `v2.1.0` tag push 완료
  - publish workflow 성공 완료
- `platform-resource`
  - 문서 정렬용 로컬 커밋 완료
  - 이번 턴 추가 배포 필요 없음
- `platform-governance`
  - 변경 없음
- `platform-integrations`
  - 문서 정렬용 로컬 커밋 완료
  - 이번 턴 추가 배포 필요 없음
- `oss-contract`
  - 문서 추가 정합화 진행 중

## 아직 남은 작업

- `platform-resource`, `platform-integrations`, `oss-contract` `main` push
- `oss-contract` 최신 문서 정합화 커밋 및 push

## 주의

- 이 문서는 로컬 작업과 원격 반영 결과를 함께 적는다.
- untracked 초안이나 과거 작업 기록은 최종 push 범위에 자동 포함하지 않는다.
- 과거 기록 중 일부 commit/tag/run id는 이전 작업 메모를 복원한 것이며, 이 문서는 그 맥락을 현재 정합 상태와 함께 보존하기 위한 용도다.
