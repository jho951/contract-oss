# 2계층 Platform 기준

`registry/layer2`는 2계층 platform 레포가 따라야 하는 공통 기준과 platform별 표준을 정의한다.

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
- `platform-integrations`는 서비스 기본 탑재 대상이 아니라 platform 사이의 선택 연결을 제공하는 bridge layer다.

## 축 요약

| 축 | 흡수 대상 | 핵심 책임 |
| --- | --- | --- |
| Platform Security | `auth`, `ip-guard`, `rate-limiter` | 요청 진입 보안 파이프라인, boundary, auth mode, IP guard, rate limit |
| Platform Governance | `audit-log`, `policy-config`, `plugin-policy-engine-config` 호환 | 구조화 감사, 정책 설정 조회, platform `GovernancePolicyPlugin` chain, feature flag config 기준 |
| Platform Resource | `file-storage`, `notification` | resource owner/kind/catalog, 저장/삭제 lifecycle, notification orchestration |
| Platform Integrations | platform 간 optional bridge | security/resource event를 governance audit으로 연결하는 optional integration platform |

## 소비 성격

| 구분 | 대상 | 소비 기준 |
| --- | --- | --- |
| 실행 플랫폼 | `platform-security`, `platform-governance`, `platform-resource` | 서비스가 starter/BOM을 직접 소비하고 내부 조립을 대체한다. |
| 연결 플랫폼 | `platform-integrations` | 두 platform을 모두 쓰고 event를 다른 platform 책임으로 전달해야 할 때만 bridge artifact를 추가한다. |

## 실무 판단 기준

- 요청 입구에서 주체, boundary, 통과/차단 여부를 판단하면 `platform-security` 책임이다.
- 요청이나 운영 사건을 감사로 남기고, 정책 값을 조회하고, platform `GovernancePolicyPlugin` chain과 위반 대응을 표준화하면 `platform-governance` 책임이다.
- 파일이나 리소스에 owner, kind, catalog, 접근, 삭제, lifecycle event가 필요하면 `platform-resource` 책임이다.
- 이미 발생한 security/resource event를 governance audit으로 이어 붙이는 것처럼 두 platform 사이의 선택 연결이면 `platform-integrations` 책임이다.
- 업무 승인, 게시글 권한, workspace membership 같은 도메인 사실 판단은 platform 책임이 아니다.
- `policy-config`, audit pipeline, feature flag config 호환 기준의 owner는 `platform-governance`다.
- `platform-governance`는 `plugin-policy-engine` 전체 runtime을 흡수하지 않고, `plugin-policy-engine-config` 호환 기준과 BOM 정렬 대상으로만 둔다.
- `platform-resource`는 file wrapper가 아니라 resource 저장, metadata/catalog, lifecycle event, notification orchestration을 묶는 runtime platform이다.
- `platform-resource`가 lifecycle event를 발행하는 것은 본체 책임이고, 그 event를 governance audit으로 기록하는 것은 `platform-integrations` 책임이다.
- `platform-security`나 `platform-resource`가 `platform-governance` 구현체를 직접 의존하면 bridge 경계를 위반한 것으로 본다.
- `platform-integrations`가 source/target platform을 대신 enable하거나 내부 구현 class를 직접 참조하면 bridge 경계를 위반한 것으로 본다.

## 기본 원칙

- 계약은 `oss-contract`가 먼저다.
- 2계층은 소비자 비즈니스 로직과 도메인 권한 판단을 포함하지 않는다.
- platform 간 연결은 각 본체 repo에 섞지 않고 `platform-integrations`의 optional bridge로 분리한다.
- 문서, build, workflow는 같은 변경 단위로 맞춘다.

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
| [structure/gradle-properties.md](structure/gradle-properties.md) | `gradle.properties`와 version pin 기준 | workflow 세부 절차 |
| [structure/build-gradle.md](structure/build-gradle.md) | `build.gradle`과 의존성/publish 구조 기준 | 실제 module 목록 |
| [structure/settings-gradle.md](structure/settings-gradle.md) | `settings.gradle` module 선언과 local substitution 기준 | 의존성 version pin 규칙 |
| [operations/ci-cd.md](operations/ci-cd.md) | `.github/workflows` build/publish 기준 | Gradle plugin/module 구조 |
| [operations/publish.md](operations/publish.md) | package publish 기준 | build/module 구조 재정의 |
| [operations/checklist.md](operations/checklist.md) | 위 기준 문서의 적용 여부 확인 | 기준 문장 재정의 |
| [standards/platform-security.md](standards/platform-security.md) | `platform-security` 전용 책임과 경계 | 다른 platform 공통 기준 |
| [standards/platform-governance.md](standards/platform-governance.md) | `platform-governance` 전용 책임과 경계 | 다른 platform 공통 기준 |
| [standards/platform-resource.md](standards/platform-resource.md) | `platform-resource` 전용 책임과 경계 | 다른 platform 공통 기준 |
| [standards/platform-integrations.md](standards/platform-integrations.md) | `platform-integrations` 전용 책임과 bridge ownership | 본체 platform 구현 기준 |

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
