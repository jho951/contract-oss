# CONTRACT_SYNC - policy-config

이 문서는 `policy-config` 레포에 반영할 동기화 기준이다.

## 기준

- 기준 SOT: `oss-contract`
- 서비스 계약 기준: `service-contract`
- 대상 레포: `policy-config`

## 확인된 역할

- 환경변수, System Properties, .properties, Map 기반 정책 조회
- 타입 안전한 `PolicyKey<T>` 조회
- Spring Boot 자동 설정 제공

## 동기화할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`

## 문구 기준

- `policy-config`는 `platform-governance`의 정책 설정 조회 구현 레포다.
- `policy-config`는 정책 값과 설정 소스를 읽는 책임만 가진다.
- `policy-config`는 정책 평가, 감사, 저장 책임을 가지지 않는다.

