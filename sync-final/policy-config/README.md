# platform-governance policy-config

`policy-config`는 `platform-governance`의 정책 설정 조회 구현 레포다.

## 책임

- 환경변수 조회
- System Properties 조회
- `.properties` 조회
- `Map` 기반 조회
- 타입 안전한 정책 키 조회
- Spring 연동

## 기준

- 공통 계약과 경계 규칙은 [oss-contract](https://github.com/jho951/oss-contract)를 따른다.
- 실제 서비스 서버의 계약은 [service-contract](https://github.com/jho951/service-contract)를 따른다.

## 권장 모듈

- `policy-config-core`
- `policy-config-spring`
- `policy-config-spring-boot-starter`
- `policy-config-common-test`

## 제외 범위

- 정책 평가 엔진
- 감사 저장
- 인증 token
- 파일 저장

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)

