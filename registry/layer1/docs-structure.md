# docs 구조 기준 - 1계층 OSS

1계층 OSS 레포의 docs 구조는 현재 구현을 흡수하되, 앞으로는 소문자 파일명과 공통 문서명을 기준으로 통일한다.

## 현재 확인된 문서 차이

- `testing-and-ci.md`와 `test-and-ci.md`가 섞여 있다.
- `audit-log`에는 `ARCHITECTURE.md`, `CONFIGURATION.md`, `RUNBOOK.md`, `TROUBLESHOOTING.md`, `USAGE.md`처럼 대문자 문서명이 섞여 있다.
- 일부 레포는 `implementation-guide.md`를 가진다.
- 레포별 특화 문서는 책임에 따라 다르다.

## 목표 구조

```text
docs/
  README.md
  architecture.md
  modules.md
  extension-guide.md
  testing-and-ci.md
  troubleshooting.md
```

## 허용되는 특화 문서

레포별 책임을 설명하기 위해 필요한 경우에만 추가한다.

- `auth`: 인증 수단, principal / token / session, 구현 가이드
- `ip-guard`: access flow, rule syntax, rule matching
- `rate-limiter`: core / spi 계약
- `audit-log`: event schema, sink, masking
- `policy-config`: source resolution
- `plugin-policy-engine`: evaluation model
- `file-storage`: backend strategy
- `notification`: delivery model, channel adapters, API model

## docs/README.md 기준

```md
# <repo-name> docs

`<repo-name>` 문서 기준은 다음과 같다.

## 범위

- `<scope-1>`
- `<scope-2>`

## 범위 밖

- platform 조립 책임
- 서비스 비즈니스 로직
- 도메인 권한 판단

## 문서

1. [architecture.md](architecture.md)
2. [modules.md](modules.md)
3. [extension-guide.md](extension-guide.md)
4. [testing-and-ci.md](testing-and-ci.md)
5. [troubleshooting.md](troubleshooting.md)
```

## docs/architecture.md 기준

```md
# Architecture

`<repo-name>`는 `<architecture-summary>` 구조를 가진다.

## 원칙

- `<principle-1>`
- `<principle-2>`

## 구성

- `<module-1>`: `<role>`
- `<module-2>`: `<role>`
```

## docs/modules.md 기준

```md
# Modules

## 모듈 목록

- `<published-module-1>`
- `<published-module-2>`

## 모듈 규칙

- 공개 좌표와 `settings.gradle` include 목록을 일치시킨다.
- API/SPI 모듈은 공개 계약만 둔다.
- core 모듈은 프레임워크 독립 핵심 구현을 둔다.
- config/builder/local 같은 보조 모듈은 책임이 분명할 때만 둔다.
- Spring/starter/platform 조립 모듈은 1계층 OSS 기본 구조에 두지 않는다.
```

## docs/extension-guide.md 기준

```md
# Extension Guide

`<repo-name>` 확장은 공개 계약을 통해서만 수행한다.

## 확장 지점

- `<extension-point-1>`
- `<extension-point-2>`

## 금지

- 내부 구현 타입 직접 의존
- platform 조립 책임 추가
- 서비스 비즈니스 로직 추가
```

## 문서명 규칙

- 파일명은 소문자 kebab-case를 사용한다.
- 테스트/CI 문서는 `testing-and-ci.md`로 통일한다.
- 트러블슈팅 문서는 `troubleshooting.md`로 통일한다.
- 대문자 docs 파일명은 새 기준으로 추가하지 않는다.
