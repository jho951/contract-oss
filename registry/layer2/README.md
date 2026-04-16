# 2계층 Platform 기준

`registry/layer2`는 2계층 platform 레포가 따라야 하는 공통 기준과 platform별 표준을 정의한다.

## 대상

- `platform-security`
- `platform-governance`
- `platform-resource`

## 의미

- 2계층은 1계층 OSS를 서비스가 붙는 조립 계층으로 묶는 private platform 레포다.
- 2계층은 3계층 application이 쉽게 가져다 쓸 수 있는 integration API를 제공한다.
- 2계층 API는 3계층 application의 최종 비즈니스 API가 아니다.
- platform 분류는 책임 축으로 정한다.

## 축 요약

| 축 | 흡수 대상 | 핵심 책임 |
| --- | --- | --- |
| Platform Security | `auth`, `ip-guard`, `rate-limiter` | 요청 진입 보안 파이프라인, boundary, auth mode, IP guard, rate limit |
| Platform Governance | `audit-log`, `policy-config`, `plugin-policy-engine` | 구조화 감사, 정책 설정 조회, 정책 평가 엔진 조립 |
| Platform Resource | `file-storage`, `notification` | resource owner/kind/catalog, 저장/삭제 lifecycle, notification orchestration |

## 기본 원칙

- 계약은 `oss-contract`가 먼저다.
- 2계층 platform은 1계층 published artifact를 exact version으로 소비한다.
- dynamic version, version range, `latest.release`, `+` 참조는 금지한다.
- 2계층은 1계층 내부 구현을 재정의하지 않는다.
- 2계층은 서비스 비즈니스 로직과 도메인 권한 판단을 포함하지 않는다.
- 문서, build, workflow는 같은 변경 단위로 맞춘다.

## 현재 구조 흡수 기준

2계층 레포의 현재 버전, 모듈, 책임은 [repositories/layer2/README.md](../../repositories/layer2/README.md)에 기록한다.
`registry/layer2`는 현재 상태 목록이 아니라, 그 상태를 판정하는 기준을 관리한다.

## platform-security 표준

- `platform-security` 표준은 [platform-security-standard.md](platform-security-standard.md)를 따른다.
- `platform-security`는 `auth`, `ip-guard`, `rate-limiter`를 조립하는 내부 비공개 플랫폼이다.
- 공개 표면은 `properties`, `customizer`, `override bean`, 역할별 starter로 제한한다.
- 회원가입, 로그인 화면, 도메인 권한 판단, 서비스별 URL, 서비스별 Redis key 규칙은 포함하지 않는다.

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

## 기준 문서

- [build-gradle.md](build-gradle.md): 2계층 build.gradle 구조 기준
- [settings-gradle.md](settings-gradle.md): 2계층 settings.gradle 구조 기준
- [ci-cd.md](ci-cd.md): 2계층 CI/CD와 publish 구조 기준
- [docs-structure.md](docs-structure.md): 2계층 docs 구조 기준
- [checklist.md](checklist.md): 2계층 공통 점검표
- [platform-security-standard.md](platform-security-standard.md): platform-security 표준
