# platform-governance plugin-policy-engine

이 저장소는 `platform-governance`의 정책 평가 엔진 구현 레포다.

## 역할

- rollout 평가
- targeting 평가
- variant 선택
- 정책 조합
- Spring Boot 연동

## 기준 문서

- 공통 계약과 경계 규칙은 [oss-contract](https://github.com/jho951/oss-contract)를 기준으로 한다.
- 실제 서비스 서버의 계약은 [service-contract](https://github.com/jho951/service-contract)를 기준으로 한다.

## 포함 범위

- policy evaluation
- rollout / targeting / variant
- 정책 조합
- Spring Boot adapter

## 제외 범위

- 정책 키 조회 저장소
- 감사 로그 저장
- 인증 token 처리
- 파일 저장

## 문서 진입점

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)

