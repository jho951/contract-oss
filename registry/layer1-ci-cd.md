# 1계층 CI/CD 표준

이 문서는 1계층 OSS 레포의 CI/CD 구조를 고정한다.

## 기본 원칙

- 테스트와 publish를 분리한다.
- tag push에서만 publish한다.
- branch push는 test / verify만 수행한다.
- publish는 GitHub Actions secret 기반으로 수행한다.
- releaseVersion은 publish job에서만 주입한다.

## 권장 구조

- `test` job
- `verify` job
- `publish` job
- `tag release` 흐름
- `Maven Central publish` 흐름

## 권장 파일

- `.github/workflows/publish.yml`
- `.github/workflows/test.yml`
- 필요하면 `.github/workflows/verify.yml`

## 공통 규칙

- workflow 이름을 가능한 한 통일한다.
- job 이름을 레포마다 다르게 만들지 않는다.
- tag 기반 릴리즈와 일반 브랜치 CI를 분리한다.
- publish job은 `-PreleaseVersion` 또는 동등한 방식으로 버전을 주입한다.

## 금지 사항

- branch push에서 publish 수행
- 레포별로 다른 publish 흐름 사용
- CI와 release 로직을 한 job에 섞기
- secret 없이 publish 실행

## 검증 항목

- test job 실행 여부
- publish job 분리 여부
- tag push에서만 publish되는지 여부
- secret 주입이 필요한 항목이 명시되는지 여부
