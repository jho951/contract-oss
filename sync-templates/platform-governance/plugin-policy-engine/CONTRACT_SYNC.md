# CONTRACT_SYNC - plugin-policy-engine

이 문서는 `plugin-policy-engine` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `plugin-policy-engine`
- 대상 역할: 정책 평가 엔진

## `plugin-policy-engine` 레포가 가져가야 하는 것

- rollout 평가
- targeting 평가
- variant 선택
- 정책 조합
- Spring 연동

## `plugin-policy-engine` 레포가 가져가면 안 되는 것

- 정책 키 조회 저장소
- 감사 저장
- 인증 token
- 파일 저장

## `oss-contract`에서 참조해야 하는 문서

- `registry/layer1-status.md`
- `registry/layer1-gradle-properties.md`
- `registry/layer1-ci-cd.md`
- `registry/layer1-maven-central.md`
- `registry/layer1-checklist.md`
- `registry/layer2-status.md`
- `CONTRACT_SYNC.md`

## plugin-policy-engine 레포에서 확인할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/evaluation-model.md`
- `gradle.properties`
- `build.gradle`
- `.github/workflows/publish.yml`

## `gradle.properties` 확인 항목

- `version`이 있는가
- `releaseVersion`이 릴리스 시에만 주입되는가
- version 키 이름이 다른 1계층 OSS와 일치하는가
- publish 좌표를 하드코딩하지 않는가

## `publish.yml` 확인 항목

- tag push에서만 publish하는가
- test / verify job과 publish job이 분리되어 있는가
- `releaseVersion`이 publish job에서만 주입되는가
- Maven Central secret을 사용하는가
- branch push에서 publish하지 않는가

## 동기화 절차

1. 정책 조합과 평가 책임을 분리한다.
2. rollout / targeting / variant의 의미를 고정한다.
3. `gradle.properties`와 `publish.yml` 구조를 `oss-contract` 표준과 맞춘다.
4. 정책 값 조회, 감사 저장, 파일 저장 책임과 섞이지 않게 한다.
5. public 계약과 내부 구현을 분리한다.

## 문구 기준

- `plugin-policy-engine`는 정책 평가 엔진 구현 레포다.
- `plugin-policy-engine`는 정책 조합과 평가를 담당한다.
- `plugin-policy-engine`는 정책 값 조회, 감사 저장, 파일 저장 책임을 가지지 않는다.

## 체크리스트

- [ ] 평가 책임이 명확한가
- [ ] rollout / targeting / variant가 분리되는가
- [ ] `gradle.properties`와 `publish.yml`이 표준 구조를 따르는가
- [ ] policy lookup과 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

## 동기화 기록

- 마지막 동기화 일자:
- 반영 요약:
- 남은 작업:
