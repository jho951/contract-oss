# plugin-policy-engine

## 기준

- GitHub: https://github.com/jho951/plugin-policy-engine
- Version: `2.0.1`
- 계층: 1계층 OSS
- registry 기준: [../../../registry/layer1/README.md](../../../registry/layer1/README.md)
- OSS 표준: [../../../registry/layer1/standards/plugin-policy-engine.md](../../../registry/layer1/standards/plugin-policy-engine.md)

## README 기준

- 공개 좌표는 실제 publish artifact와 일치해야 한다.
- `무엇을 제공하나`는 `settings.gradle` include 목록과 일치해야 한다.
- 책임 경계에는 1계층 책임과 2계층 platform 책임을 명확히 나눈다.
- SOT 내부 동기화 문서를 레포 README에 안내하지 않는다.

## 책임

- 기능 플래그 평가 모델
- allow / deny 타겟팅
- 속성 기반 eligibility
- 결정론적 rollout
- variant 선택
- `FlagStore` SPI와 순수 Java 조립 API

## 현재 모듈

- `plugin-policy-engine-api`
- `plugin-policy-engine-core`
- `plugin-policy-engine-config`

## 현재 문서

- `README.md`
- `docs/readme.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/implementation-guide.md`
- `docs/test-and-ci.md`
- `docs/troubleshooting.md`

## 문서 기준

- 파일명은 소문자 `kebab-case`를 사용한다.
- 테스트/CI 문서는 `docs/test-and-ci.md`로 통일한다.
- 대문자 docs 파일명은 새 기준으로 추가하지 않는다.
- `docs/implementation-guide.md`는 레포 책임에 필요한 경우에만 둔다.
- 레포별 특화 문서는 OSS 표준의 책임 범위 안에서만 둔다.

## 현재 운영 파일

- `.github/ISSUE_TEMPLATE/*`
- `.github/pull_request_template.md`
- `.github/workflows/build.yml`
- `.github/workflows/publish.yml`
- `CONTRIBUTING.md`
- `LICENSE`
- `SECURITY.md`
- `SUPPORT.md`

## 정리 후보

- 없음
