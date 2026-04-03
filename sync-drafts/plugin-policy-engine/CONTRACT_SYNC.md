# CONTRACT_SYNC - plugin-policy-engine

이 문서는 `plugin-policy-engine` 레포에 반영할 동기화 기준이다.

## 기준

- 기준 SOT: `oss-contract`
- 서비스 계약 기준: `service-contract`
- 대상 레포: `plugin-policy-engine`

## 확인된 역할

- rollout / targeting / variant 평가용 정책 엔진
- Spring Boot 지원
- file store 기반 저장 모듈 포함

## 동기화할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`

## 문구 기준

- `plugin-policy-engine`는 `platform-governance`의 정책 평가 엔진 구현 레포다.
- `plugin-policy-engine`는 정책 조합과 평가를 담당한다.
- `plugin-policy-engine`는 정책 값 조회, 감사 저장, 파일 저장 책임을 가지지 않는다.

