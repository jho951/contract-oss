# auth

## 계층

- 1계층 OSS
- `platform-security`로 흡수될 기준 레포

## 상태

- 존재
- 기준 레포

## 소유 기준

- `oss-contract`
- `sync-final/auth/CONTRACT_SYNC.md`

## 역할

- 인증 처리
- principal / token / session
- JWT / OAuth2 / Spring 연동

## 현재

- 멀티모듈 인증 OSS
- Maven Central 배포 대상
- tag 기반 publish 사용

## 모듈

- `auth-core`
- `auth-jwt`
- `auth-session`
- `auth-hybrid`
- `auth-spring`
- `auth-spring-boot-starter`
- `auth-common-test`

## 목표

- `platform-security`의 표준 인증 구현 레포
- 1계층 공통 Gradle / publish 표준 적용
- 문서와 배포 흐름의 완전한 통일

## 변경 포인트

- 루트 `build.gradle`
- `settings.gradle`
- `.github/workflows/publish.yml`
- `docs/`

## 배포

- Maven Central
- tag 기반 publish
- GitHub Actions `publish.yml`

## 동기화 기준

- [sync-final/auth/CONTRACT_SYNC.md](../sync-final/auth/CONTRACT_SYNC.md)

