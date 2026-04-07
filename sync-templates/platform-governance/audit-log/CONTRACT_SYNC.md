# CONTRACT_SYNC - audit-log

이 문서는 `audit-log` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `audit-log`
- 대상 역할: 구조화된 감사 로그 공통 모듈

## `audit-log` 레포가 가져가야 하는 것

- actor
- occurredAt
- clientIp
- action
- resource
- result
- 보안 감사와 운영 추적을 위한 표준 이벤트
- Spring Boot starter

## `audit-log` 레포가 가져가면 안 되는 것

- 정책 엔진 평가
- 인증 토큰 발급
- 파일 저장
- 서비스별 비즈니스 로직
- 감사 로그 외의 정책 카탈로그 책임

## `oss-contract`에서 참조해야 하는 문서

- `registry/layer1-status.md`
- `registry/layer1-gradle-properties.md`
- `registry/layer1-ci-cd.md`
- `registry/layer1-maven-central.md`
- `registry/layer1-checklist.md`
- `registry/layer2-status.md`
- `CONTRACT_SYNC.md`

## audit-log 레포에서 확인할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
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

1. 감사 이벤트 표준 필드를 고정한다.
2. 보안 감사와 운영 추적 재사용 가능성을 분명히 한다.
3. `gradle.properties`와 `publish.yml` 구조를 `oss-contract` 표준과 맞춘다.
4. policy/security/storage 책임과 섞이지 않도록 한다.
5. public 계약과 내부 구현을 분리한다.

## 문구 기준

- `audit-log`는 구조화된 감사 로그 공통 모듈이다.
- `audit-log`는 보안 감사와 운영 추적에 재사용된다.
- `audit-log`는 정책 결정 엔진이 아니다.

## 체크리스트

- [ ] 표준 필드가 일관되게 적혀 있는가
- [ ] starter와 core의 역할이 분리되어 있는가
- [ ] `gradle.properties`와 `publish.yml`이 표준 구조를 따르는가
- [ ] policy/security/storage 책임과 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

## 동기화 기록

- 마지막 동기화 일자:
- 반영 요약:
- 남은 작업:
