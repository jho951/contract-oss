# platform-governance plugin-policy-engine

`plugin-policy-engine`는 `platform-governance`의 정책 평가 엔진 구현 레포다.

## 책임

- rollout 평가
- targeting 평가
- variant 선택
- 정책 조합
- Spring 연동

## 권장 모듈

- `plugin-policy-engine-core`
- `plugin-policy-engine-spring`
- `plugin-policy-engine-spring-boot-starter`
- `plugin-policy-engine-common-test`

## 모듈 설명

- `plugin-policy-engine-core`: 정책 평가와 조합
- `plugin-policy-engine-spring`: Spring 어댑터
- `plugin-policy-engine-spring-boot-starter`: 소비 진입점
- `plugin-policy-engine-common-test`: 테스트 지원

## 제외 범위

- 정책 키 조회 저장소
- 감사 저장
- 인증 token
- 파일 저장

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)
5. [docs/evaluation-model.md](docs/evaluation-model.md)
