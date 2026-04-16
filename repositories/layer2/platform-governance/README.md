# platform-governance

## 기준

- GitHub: https://github.com/jho951/platform-governance
- Version: `1.0.0`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)

## 흡수 대상

- `audit-log`
- `policy-config`
- `plugin-policy-engine`

## 책임

- 구조화 감사
- 정책 설정 조회
- 정책 평가 엔진 조립
- 1계층 governance OSS 배포본 소비 기준 고정
- governance integration API 제공

## 현재 모듈

- `platform-governance-bom`
- `platform-governance-api`
- `platform-governance-audit`
- `platform-governance-config`
- `platform-governance-core`
- `platform-governance-engine`
- `platform-governance-spring`
- `platform-governance-spring-boot-starter`
- `platform-governance-common-test`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/configuration.md`
- `docs/dependency-basis.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/governance-model.md`
- `docs/private-publish.md`

## 정리 후보

- `.DS_Store` 제거
- `CONTRACT_SYNC.md` 제거
- `gradle.properties` 추가 여부 확인
