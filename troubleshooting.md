# OSS / Platform Troubleshooting

이 문서는 2026-04-23 기준으로 1계층 OSS와 2계층 platform 경계를 맞추는 과정에서 실제로 확인한 문제, 변경 이유, 수정 내역, 현재 상태를 정리한 기록이다.

이번 턴에서 새로 확인한 내용뿐 아니라, 이전 작업에서 남겨두지 못했던 release/publish 이력과 실패 원인도 함께 적는다.

## 대상 레포

- `oss-contract`
- `platform-security`
- `platform-resource`
- `platform-governance`
- `platform-integrations`

## 현재 published 기준

- `platform-security`: `3.0.1`
- `platform-resource`: `3.0.1`
- `platform-governance`: `3.0.1`
- `platform-integrations`: `3.0.1`
- `platform-runtime-bom`: `3.0.1`
- `platform-security-governance-bridge`: `3.0.1`
- `platform-resource-governance-bridge`: `3.0.1`

## 읽는 방법

- 이 문서 아래의 `2.x`, `1.x` 버전과 publish 실패 이력은 migration history로 남긴 것이다.
- 현재 stage-5 baseline과 소비 기준은 `3.0.1` release train 문서와 각 repository README를 source-of-truth로 본다.

## 현재 stage-5 계약 요약

- service consumer는 `starter + sanctioned add-on + public SPI`만 기준으로 붙고, `core/internal/autoconfigure` 구현 세부사항을 직접 알지 않는다.
- `platform-security`는 base `platform-security-starter`와 optional add-on(`platform-security-auth-bridge-starter`, `platform-security-ratelimit-bridge-starter`, `platform-security-web-api`, `platform-security-legacy-compat`, `platform-security-hybrid-web-adapter`, `platform-security-client`) 구조를 사용한다.
- `platform-governance`의 공식 감사 출력 SPI는 `AuditSink`이고, `AuditLogRecorder`는 governance internal adapter seam으로만 본다.
- `platform-resource`와 `platform-governance` starter는 stage-5 compile classpath 기준에서 core/engine/adapter 구현을 서비스 compile surface에 직접 새지 않는다.
- cross-platform 조합과 bridge version은 `platform-runtime-bom:3.0.1` release train을 source-of-truth로 본다.

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

## 이번 턴에서 실제로 발생한 오류

### 1. `platform-governance-samples` 부팅 실패

- 증상:
  - `NoClassDefFoundError: io.github.jho951.platform.governance.spring.PlatformGovernanceProperties`
  - `Error processing condition on io.github.jho951.platform.governance.spring.PlatformGovernanceAutoConfiguration.platformGovernanceClock`
- 발생 맥락:
  - stage-5 compile surface 정리 후 `ApplicationContextRunner` 기반 sample consumer를 다시 검증하는 과정에서 발생했다.
- 원인:
  - `platform-governance-autoconfigure` 하위 build output이 stale 상태였고, `@ConditionalOnMissingBean` 타입 추론이 필요한 시점에 `PlatformGovernanceProperties`가 누락된 것처럼 보였다.
- 조치:
  - `./gradlew :platform-governance-autoconfigure:clean :platform-governance-autoconfigure:compileJava`
  - 이후 `./gradlew :platform-governance-samples:test` 재실행
- 판단:
  - stage-5 starter 계약 자체의 설계 결함이 아니라 local build artifact 불일치였다.

### 2. `platform-integrations` publish workflow가 `platform-runtime-bom`을 처리하지 못함

- 증상:
  - module publish workflow가 모든 모듈에 `:module:test`를 강제했다.
  - `platform-runtime-bom`은 `java-platform` 모듈이라 `test` task가 없어 release train publish가 실패하는 구조였다.
- 원인:
  - bridge module과 release-train BOM module을 같은 검증 경로로 가정했다.
- 조치:
  - workflow가 먼저 `:module:test` 존재 여부를 dry-run으로 확인하고, 없으면 `:module:check`로 fallback 하도록 수정했다.
- 영향:
  - `platform-runtime-bom:3.0.1`이 `platform-integrations`의 공식 publish surface로 정리됐다.

### 3. included-build 병렬 검증 시 build directory delete 충돌

- 증상:
  - `Execution failed for task ':platform-governance:platform-governance-autoconfigure:compileJava'`
  - `Unable to delete directory .../platform-governance-spring/build/classes/java/main`
- 발생 맥락:
  - `platform-integrations` smoke consumer를 composite build로 검증하는 동안, 같은 included build를 다른 Gradle 실행이 같이 건드렸다.
- 원인:
  - 동일한 included build tree를 병렬 Gradle invocation이 동시에 mutate했다.
- 조치:
  - 검증을 순차 실행으로 바꿔 재실행했고, 재현 없이 통과했다.
- 판단:
  - release artifact나 public surface 문제는 아니고 local verification orchestration 문제였다.

## 3.0.1 기준 실제 변경

### 1. `platform-security`

- stage-5 소비 기준으로 `starter + sanctioned add-on + public SPI` 구조를 닫았다.
- `SecurityPolicy` additive 합성, ingress contributor SPI, `platform-security-web-api`, optional bridge starter, hybrid runtime surface를 공식 표면으로 정리했다.
- base starter에서 `platform-security-client`를 분리해 inbound runtime과 outbound propagation을 구분했다.
- `main` push와 `v3.0.1` publish가 완료됐다.
- publish run:
  - https://github.com/jho951/platform-security/actions/runs/24817534813

### 2. `platform-resource`

- starter/autoconfigure compile classpath에서 `core` 구현이 서비스 compile surface로 새지 않도록 정리했다.
- `platform-resource-sample-consumer` 기준으로 public API/SPI만으로 부팅과 저장 흐름이 성립하도록 맞췄다.
- relay/customizer/module 문서도 실제 publish surface와 `3.0.1` 기준으로 정렬했다.
- `main` push와 `v3.0.1` publish가 완료됐다.
- publish run:
  - https://github.com/jho951/platform-resource/actions/runs/24817536795

### 3. `platform-governance`

- starter compile surface에서 내부 adapter/core/engine 누수를 줄이고, 서비스 공식 SPI를 `AuditSink`, `PolicyConfigSource`, `GovernanceDecisionEngine`, `ViolationHandler` 기준으로 다시 고정했다.
- mainline auto-config에서 `AuditLogRecorder` compat fan-out을 extension point처럼 다루지 않는 방향으로 정리했다.
- sample consumer 기준으로 classpath closure를 다시 확인했고, `v3.0.1` publish가 완료됐다.
- publish run:
  - https://github.com/jho951/platform-governance/actions/runs/24817536135

### 4. `platform-integrations`

- `platform-runtime-bom`을 supported release train SoT로 추가했다.
- `platform-security-governance-bridge`와 `platform-resource-governance-bridge`를 `3.0.1` release train으로 다시 정렬했다.
- module-scoped publish workflow가 BOM module도 처리할 수 있도록 수정했다.
- publish run:
  - `platform-runtime-bom`: https://github.com/jho951/platform-integrations/actions/runs/24817847857
  - `platform-security-governance-bridge`: https://github.com/jho951/platform-integrations/actions/runs/24817848443
  - `platform-resource-governance-bridge`: https://github.com/jho951/platform-integrations/actions/runs/24817849131

### 5. `oss-contract`

- `repositories/layer2/README.md`와 각 repo 상태 문서를 `3.0.1` release train 기준으로 맞췄다.
- `registry/layer2/standards/platform-security.md`, `platform-governance.md`, `platform-resource.md`, `platform-integrations.md`를 stage-5 소비 경계 기준으로 정렬했다.
- 이 문서 `troubleshooting.md`를 이번 수정 과정의 실제 오류, 해결 방법, publish 결과까지 포함하는 cross-repo SoT로 재정리했다.

## 검증

### `platform-security`

성공:

```bash
./gradlew verifyPublishedSurface verifyStarterContract :platform-security-sample-consumer:test
```

### `platform-governance`

성공:

```bash
./gradlew :platform-governance-autoconfigure:clean :platform-governance-autoconfigure:compileJava
./gradlew :platform-governance-samples:test
```

### `platform-resource`

성공:

```bash
./gradlew :platform-resource-sample-consumer:test
```

### `platform-integrations`

성공:

```bash
./gradlew verifyPublishedSurface verifyStarterContract :platform-stack-smoke-consumer:test -PuseLocalPlatform=true
```

## 지금 시점의 정합 상태

- `platform-security`, `platform-resource`, `platform-governance`, `platform-integrations`의 current published baseline은 모두 `3.0.1`이다.
- supported 조합 version은 `platform-runtime-bom:3.0.1`을 source-of-truth로 본다.
- `oss-contract`의 layer2 표준과 repository 상태 문서는 위 baseline 기준으로 다시 정렬됐다.
- 서비스 repo의 version pin과 platform 소비 방향도 `3.0.1` release train 기준으로 정리된 상태다.
- 다만 published artifact만 사용한 서비스 재검증, Docker image build, container 기동 smoke, 서비스 간 end-to-end 호출 검증은 이 문서 범위 밖의 별도 검증 과제로 남는다.

## push / publish 관점 현재 상태

- `platform-security`
  - `main` push 완료
  - `v3.0.1` tag push 완료
  - publish workflow 성공
- `platform-resource`
  - `main` push 완료
  - `v3.0.1` tag push 완료
  - publish workflow 성공
- `platform-governance`
  - `main` push 완료
  - `v3.0.1` tag push 완료
  - publish workflow 성공
- `platform-integrations`
  - `main` push 완료
  - `platform-runtime-bom/v3.0.1` tag push 완료
  - `platform-security-governance-bridge/v3.0.1` tag push 완료
  - `platform-resource-governance-bridge/v3.0.1` tag push 완료
  - 각 module publish workflow 성공
- `oss-contract`
  - layer2 표준, repo 상태, troubleshooting 기록을 현재 publish baseline 기준으로 정렬 완료

## 주의

- 이 문서는 로컬 작업과 원격 반영 결과를 함께 적는다.
- 이 문서 위쪽의 `2.x`, `1.x` 버전 이력은 historical migration record이며 현재 baseline이 아니다.
- 일부 실패는 public surface 결함이 아니라 workflow/local build artifact 문제였고, 각 항목에 그렇게 구분해 적었다.
