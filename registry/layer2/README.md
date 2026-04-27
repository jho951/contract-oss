# 2계층 Platform 기준

`registry/layer2`는 2계층 platform 레포가 따라야 하는 공통 기준과 platform별 표준을 정의한다.

목표 구조는 [l5-target-architecture.md](l5-target-architecture.md), 실제 전환 순서는 [l5-migration-plan.md](l5-migration-plan.md)에서 관리한다.

## 대상

- `platform-security`
- `platform-governance`
- `platform-resource`
- `platform-integrations`

## 의미

- 2계층은 1계층 OSS를 소비 애플리케이션이 붙는 조립 계층으로 묶는 private platform 레포다.
- 2계층은 platform 소비자가 쉽게 가져다 쓸 수 있는 integration API를 제공한다.
- 2계층 API는 최종 비즈니스 API가 아니다.
- platform 분류는 책임 축으로 정한다.
- `platform-security`, `platform-governance`, `platform-resource`는 서비스가 직접 소비하는 runtime platform이다.
- `platform-integrations`는 서비스 바깥으로 나가는 알림, 외부 연동, 이벤트 발행을 표준화하는 outbound platform이다.

## 축 요약

| 축 | 흡수 대상 | 핵심 책임 |
| --- | --- | --- |
| Platform Security | `auth`, `ip-guard`, `rate-limiter` | 인증, 인가, JWT, 세션, ingress 보안 집행 |
| Platform Governance | `audit-log`, `policy-config`, `plugin-policy-engine` 호환 | 감사, 정책, 운영 통제, 위반 대응 |
| Platform Resource | `file-storage`, `notification` | 파일과 리소스 저장, metadata, lifecycle, access |
| Platform Integrations | `notification` 중심 outbound OSS | 알림, 외부 연동, 이벤트 발행, retry, idempotency |

## 소비 성격

| 구분 | 대상 | 소비 기준 |
| --- | --- | --- |
| 실행 플랫폼 | `platform-security`, `platform-governance`, `platform-resource` | 서비스가 starter/BOM을 직접 소비하고 내부 조립을 대체한다. |
| outbound 플랫폼 | `platform-integrations` | 서비스 밖으로 나가는 전달과 연동 흐름을 표준화한다. |

## 실무 판단 기준

- 요청 입구에서 주체, boundary, 인증, 인가, 통과/차단을 집행하면 `platform-security` 책임이다.
- 정책 값을 읽고, audit을 남기고, 운영 기준과 위반 대응을 표준화하면 `platform-governance` 책임이다.
- 파일이나 리소스에 owner, kind, catalog, 접근, 저장, 삭제, lifecycle event가 필요하면 `platform-resource` 책임이다.
- 메일, 문자, 푸시, webhook, outbound event처럼 서비스 밖으로 나가는 전달 흐름을 표준화하면 `platform-integrations` 책임이다.
- 업무 승인, 게시글 권한, workspace membership 같은 도메인 사실 판단은 platform 책임이 아니다.
- `policy-config`, audit pipeline, feature flag config 호환 기준의 owner는 `platform-governance`다.
- `platform-governance`는 `plugin-policy-engine` 전체 runtime을 흡수하지 않고, policy engine 연동 기준과 BOM 정렬 대상으로만 둔다.
- `platform-resource`는 file wrapper가 아니라 resource 저장, metadata/catalog, lifecycle event, notification orchestration을 묶는 runtime platform이다.
- `platform-resource`가 lifecycle event를 발행하는 것은 본체 책임이고, 그 이후 알림이나 외부 전달은 `platform-integrations`와 연결할 수 있다.
- `platform-security`, `platform-resource`, `platform-integrations`는 `platform-governance`의 정책과 audit 기준을 소비할 수 있지만, 순환 의존을 만들면 안 된다.

## 기본 원칙

- 계약은 `oss-contract`가 먼저다.
- 2계층은 소비자 비즈니스 로직과 도메인 권한 판단을 포함하지 않는다.
- outbound 실행 흐름은 서비스마다 따로 구현하지 않고 `platform-integrations`로 모은다.
- 문서, build, workflow는 같은 변경 단위로 맞춘다.

## 엄격한 분리 기준

가장 엄격한 형태의 2계층 구조는 아래를 기준으로 본다.

```text
[1계층 OSS]
auth / session / rate-limiter / file-storage / notification / audit-log / policy-config
        ↑
        │  adapter만 1계층과 platform을 함께 안다
        │
[adapter layer]
auth-platform-adapter
ratelimiter-platform-adapter
filestorage-platform-adapter
notification-platform-adapter
auditlog-platform-adapter
policyconfig-platform-adapter
        ↑
        │  service는 platform 타입만 안다
        │
[2계층 platform]
platform-api
platform-ports
platform-core
platform-starter
platform-policy
```

- `platform core/starter/policy`는 1계층 타입을 직접 import하지 않는다.
- 1계층 타입과 platform port를 함께 아는 코드는 adapter layer에만 둔다.
- 서비스는 platform starter와 platform port만 소비하고, 1계층 타입을 직접 import하지 않는다.
- adapter를 같은 repo 안에 두면 아키텍처 경계 분리는 성립하지만, repo 전체가 1계층 무지라고 보지는 않는다.
- repo 수준까지 완전 분리를 원하면 adapter source도 platform repo 밖으로 분리해야 한다.

## Public Surface Rule

- platform public API는 100% platform-owned 타입으로 닫는다.
- 공개 시그니처에 raw `com.auth.*`, `RateLimiter`, `FileStorage`, `NotificationDispatcher`, `GovernanceAuditRecorder`, `PolicyConfig*` 같은 1계층 타입이 나오면 안 된다.
- auto-configuration과 starter 조건도 `@ConditionalOnBean(Platform...Port.class)`처럼 platform port 기준으로만 건다.
- 1계층 bean을 감지하고 platform port 구현으로 바꾸는 일은 adapter auto-configuration의 책임으로 본다.

## Runtime View Rule

platform-owned 타입은 허용하되, 그 목적은 1계층 핵심 모델의 대체가 아니라 2계층 runtime 조립 언어여야 한다.

- 허용:
  - `SecurityRequest`
  - `SecurityContext`
  - `PlatformRateLimitRequest`
  - `PlatformRateLimitDecision`
  - `ResourceLifecycleEvent`
  - `IssuedCredentialView`
- 금지:
  - 1계층 `Principal`을 사실상 다시 정의한 새 canonical principal 모델
  - `TokenService`, `FileStorage`, `NotificationDispatcher`를 그대로 복제한 platform service 계약
  - 1계층 도메인 계약을 이름만 바꿔서 다시 노출하는 wrapper API

즉 2계층 DTO는 orchestration/runtime view여야 하고, 1계층 도메인 계약의 복제품이 되면 안 된다.

## 플랫폼 공통 정합성 기준

- runtime platform인 `platform-security`, `platform-governance`, `platform-resource`는 production profile 기본값을 동일하게 가져간다.
- production profile 기본값은 `["prod", "production"]`로 통일한다.
- runtime platform의 fail-fast는 service role/preset을 고려한 역할별 규칙이어야 한다.
- platform 소비 서비스가 1계층 OSS 타입을 직접 맞춰 노출해야만 동작하는 구조는 허용하지 않는다.
- platform 내부에서만 1계층 OSS를 adapter로 흡수하고, 소비자에게는 platform 소유 port/adapter만 노출한다.
- README, quickstart, ownership, usage 예시 버전은 각 repository의 현재 `release_version`과 exact dependency pin에 맞춰 유지한다.

## 현재 구조 흡수 기준

2계층 레포의 현재 버전, 모듈, 책임은 [repositories/layer2/README.md](../../repositories/layer2/README.md)에 기록한다.
`registry/layer2`는 현재 상태 목록이 아니라, 그 상태를 판정하는 기준을 관리한다.

## 문서 책임

| 문서 | 책임 | 쓰지 않는 것 |
| --- | --- | --- |
| [README.md](README.md) | 2계층 정의, 책임 축, 문서 위치 | 세부 build/module/docs/workflow 규칙 |
| [l5-target-architecture.md](l5-target-architecture.md) | 1계층 OSS -> 2계층 플랫폼 -> 3계층 서비스 목표 구조 | 현재 구현의 역사 설명 |
| [l5-migration-plan.md](l5-migration-plan.md) | 목표 구조로 옮기는 순서 | 현재 구현의 역사 설명 |
| [structure/gradle-properties.md](structure/gradle-properties.md) | `gradle.properties`와 version pin 기준 | workflow 세부 절차 |
| [structure/build-gradle.md](structure/build-gradle.md) | `build.gradle`과 의존성/publish 구조 기준 | 실제 module 목록 |
| [structure/settings-gradle.md](structure/settings-gradle.md) | `settings.gradle` module 선언과 local substitution 기준 | 의존성 version pin 규칙 |
| [operations/ci-cd.md](operations/ci-cd.md) | `.github/workflows` build/publish 기준 | Gradle plugin/module 구조 |
| [operations/publish.md](operations/publish.md) | package publish 기준 | build/module 구조 재정의 |
| [operations/checklist.md](operations/checklist.md) | 위 기준 문서의 적용 여부 확인 | 기준 문장 재정의 |
| [standards/platform-security.md](standards/platform-security.md) | `platform-security` 전용 책임과 경계 | 다른 platform 공통 기준 |
| [standards/platform-governance.md](standards/platform-governance.md) | `platform-governance` 전용 책임과 경계 | 다른 platform 공통 기준 |
| [standards/platform-resource.md](standards/platform-resource.md) | `platform-resource` 전용 책임과 경계 | 다른 platform 공통 기준 |
| [standards/platform-integrations.md](standards/platform-integrations.md) | `platform-integrations` 전용 책임과 outbound ownership | 본체 platform 구현 기준 |

## 반영 기준

- 한 번에 한 platform 레포를 반영한다.
- 1계층 버전 변경은 platform 의존성 pin과 같이 확인한다.
- 모듈명이 다르면 `settings.gradle`을 먼저 확인한다.
- 의존성 반영이 꼬이면 `build.gradle`과 version pin을 먼저 확인한다.
- 파일 하나씩 반영이 꼬이면 `repositories/layer2/<repo>`와 대상 레포를 line-by-line 비교한다.

## 적용 기준

- `repositories/layer2`는 2계층 레포 카탈로그와 레포별 기준 문서 집합이다.
- `registry/layer2`는 2계층 공통 기준과 platform별 표준을 담는다.
- 문서 외 산출물이 생기면 제거한다.
