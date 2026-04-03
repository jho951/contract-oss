# 1계층 OSS 구조 표준

이 문서는 `auth`의 실제 구조를 기준으로 1계층 OSS 레포의 공통 구조를 정의한다.

## 관찰된 `auth` 구조

`auth` 레포는 다음 요소를 가진다.

- 루트 README
- Gradle 기반 멀티모듈 구조
- `docs/` 문서 디렉터리
- `samples/` 데모 디렉터리
- `auth-core`
- `auth-common-test`
- `auth-jwt`
- `auth-session`
- `auth-hybrid`
- `auth-spring`
- `auth-spring-boot-starter`
- GitHub Actions publish workflow

## 표준 결론

1계층 OSS는 `auth`에서 확인된 멀티모듈 패턴을 기준으로 통일한다.

- `core`: 도메인 규칙과 SPI
- `strategy`: 선택 가능한 구현 변형
- `spring`: 프레임워크 바인딩
- `spring-boot-starter`: 자동 설정 진입점
- `common-test`: 테스트 지원
- `api`: 외부에 노출할 계약이 분리되어야 할 때만 사용
- `autoconfigure`: starter와 분리해서 자동 설정을 관리할 때만 사용

## 공통 구조 원칙

- 루트에는 레포의 목적과 배포 방식만 둔다.
- 계약과 문서는 `oss-contract`와 동기화한다.
- 구현은 모듈 단위로 쪼갠다.
- Spring 연동은 adapter와 starter로 분리한다.
- 테스트 지원은 production path와 분리한다.
- 샘플 앱은 선택 사항이다.

## 권장 루트 레이아웃

- `README.md`
- `CONTRACT_SYNC.md` 또는 레포별 동기화 문서
- `build.gradle`
- `settings.gradle`
- `gradle.properties`
- `gradlew`
- `gradlew.bat`
- `gradle/wrapper/*`
- `.github/workflows/*`
- `docs/`
- `samples/` 또는 `examples/`

## 권장 문서 레이아웃

- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- 필요 시 `docs/configuration.md`
- 필요 시 `docs/api.md`
- 필요 시 `docs/security.md`
- 필요 시 `docs/testing-and-ci.md`
- 필요 시 `docs/release.md`

## 권장 모듈 레이아웃

### 공통형

- `<name>-core`
- `<name>-spring`
- `<name>-spring-boot-starter`
- `<name>-common-test`

### 계약 분리형 추가 모듈

- `<name>-api`
- `<name>-autoconfigure`

### 전략형 추가 모듈

- `<name>-jwt`
- `<name>-session`
- `<name>-hybrid`
- `<name>-redis`

## 통일 규칙

- 모듈 이름은 역할이 드러나야 한다.
- core는 도메인 규칙과 SPI를 담는다.
- spring은 프레임워크 바인딩을 담는다.
- starter는 자동 구성을 담는다.
- api는 외부 계약이 구현과 분리되어야 할 때만 둔다.
- autoconfigure는 starter 내부에서 자동 설정이 커질 때 분리한다.
- optional strategy는 별도 모듈로 분리한다.
- 샘플은 본체와 분리한다.

## auth 기준으로 본 권장 판단

- `auth-core`는 유지한다.
- `auth-jwt`, `auth-session`, `auth-hybrid`는 전략 모듈로 유지한다.
- `auth-spring`, `auth-spring-boot-starter`는 유지한다.
- `auth-common-test`는 테스트 전용으로 유지한다.
- `samples/`는 문서와 분리된 데모로 유지한다.

## 다른 1계층 OSS에 적용할 방식

- 보안 계층은 auth와 같은 멀티모듈 패턴을 따른다.
- 감사/정책/스토리지는 필요한 경우 api/core/spring/autoconfigure/starter로 분리한다.
- 샘플이 필요 없으면 `samples/`는 생략한다.
- 문서 레이아웃은 공통화한다.

## 레포별 권장 모듈

| 레포 | 권장 모듈 |
| --- | --- |
| `auth` | `auth-core`, `auth-jwt`, `auth-session`, `auth-hybrid`, `auth-spring`, `auth-spring-boot-starter`, `auth-common-test` |
| `ip-guard` | `ip-guard-core`, `ip-guard-spring`, `ip-guard-spring-boot-starter`, `ip-guard-common-test` |
| `rate-limiter` | `rate-limiter-core`, `rate-limiter-redis`, `rate-limiter-spring`, `rate-limiter-spring-boot-starter`, `rate-limiter-common-test` |
| `audit-log` | `audit-log-api`, `audit-log-core`, `audit-log-autoconfigure`, `audit-log-spring-boot-starter`, `audit-log-common-test` |
| `policy-config` | `policy-config-core`, `policy-config-spring`, `policy-config-spring-boot-starter`, `policy-config-common-test` |
| `plugin-policy-engine` | `plugin-policy-engine-core`, `plugin-policy-engine-spring`, `plugin-policy-engine-spring-boot-starter`, `plugin-policy-engine-common-test` |
| `file-storage-module` | `file-storage-api`, `file-storage-core`, `file-storage-spring`, `file-storage-spring-boot-starter`, `file-storage-common-test` |
| `notification` | 미정, 기능이 생긴 뒤 재분류 |

## 모듈 통일 규칙

- `*-core`는 반드시 도메인 규칙 중심으로 둔다.
- `*-spring-boot-starter`는 애플리케이션 진입점 역할만 한다.
- `*-spring`은 프레임워크 바인딩만 둔다.
- `*-autoconfigure`는 필요한 경우에만 둔다.
- `*-common-test`는 테스트 픽스처만 둔다.
- `*-api`는 구현과 분리된 외부 계약이 있을 때만 둔다.
