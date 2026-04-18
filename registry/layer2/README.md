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

## 축 요약

| 축 | 흡수 대상 | 핵심 책임 |
| --- | --- | --- |
| Platform Security | `auth`, `ip-guard`, `rate-limiter` | 요청 진입 보안 파이프라인, boundary, auth mode, IP guard, rate limit |
| Platform Governance | `audit-log`, `policy-config`, `plugin-policy-engine` | 구조화 감사, 정책 설정 조회, 정책 평가 엔진 조립 |
| Platform Resource | `file-storage`, `notification` | resource owner/kind/catalog, 저장/삭제 lifecycle, notification orchestration |
| Platform Integrations | platform 간 optional bridge | security/resource event를 governance audit으로 연결하는 optional integration platform |

## 실무 판단 기준

- 요청 입구에서 주체, boundary, 통과/차단 여부를 판단하면 `platform-security` 책임이다.
- 요청이나 운영 사건을 감사로 남기고, 정책 값을 조회하고, 정책 평가/위반 대응을 표준화하면 `platform-governance` 책임이다.
- 파일이나 리소스에 owner, kind, catalog, 접근, 삭제, lifecycle event가 필요하면 `platform-resource` 책임이다.
- 이미 발생한 security/resource event를 governance audit으로 이어 붙이는 것처럼 두 platform 사이의 선택 연결이면 `platform-integrations` 책임이다.
- 업무 승인, 게시글 권한, workspace membership 같은 도메인 사실 판단은 platform 책임이 아니다.

## 기본 원칙

- 계약은 `oss-contract`가 먼저다.
- 2계층은 소비자 비즈니스 로직과 도메인 권한 판단을 포함하지 않는다.
- platform 간 연결은 각 본체 repo에 섞지 않고 `platform-integrations`의 optional bridge로 분리한다.
- 문서, build, workflow는 같은 변경 단위로 맞춘다.

## 현재 구조 흡수 기준

2계층 레포의 현재 버전, 모듈, 책임은 [repositories/layer2/README.md](../../repositories/layer2/README.md)에 기록한다.
`registry/layer2`는 현재 상태 목록이 아니라, 그 상태를 판정하는 기준을 관리한다.

## 문서 책임

| 문서 | 책임 | 쓰지 않는 것 |
| --- | --- | --- |
| [README.md](README.md) | 2계층 정의, 책임 축, 문서 위치 | 세부 build/module/docs/workflow 규칙 |
| [build-gradle.md](build-gradle.md) | `build.gradle`과 의존성/publish 구조 기준 | 실제 module 목록 |
| [settings-gradle.md](settings-gradle.md) | `settings.gradle` module 선언과 local substitution 기준 | 의존성 version pin 규칙 |
| [ci-cd.md](ci-cd.md) | `.github/workflows` build/publish 기준 | Gradle plugin/module 구조 |
| [docs-structure.md](docs-structure.md) | platform repo의 docs 구조 기준 | build/workflow 기준 |
| [platform-security-standard.md](platform-security-standard.md) | `platform-security` 전용 책임과 경계 | 다른 platform 공통 기준 |
| [platform-integrations-standard.md](platform-integrations-standard.md) | `platform-integrations` 전용 책임과 bridge ownership | 본체 platform 구현 기준 |
| [checklist.md](checklist.md) | 위 기준 문서의 적용 여부 확인 | 기준 문장 재정의 |

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
