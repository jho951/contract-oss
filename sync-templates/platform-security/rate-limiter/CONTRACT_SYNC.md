# CONTRACT_SYNC - rate-limiter

이 문서는 `rate-limiter` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `rate-limiter`
- 대상 역할: 요청량 제한, in-memory/Redis 제한, Spring 연동

## `rate-limiter` 레포가 가져가야 하는 것

- IP / 사용자 ID / API 키 기준 제한
- in-memory token bucket
- Redis 기반 분산 제한
- Spring 연동

## `rate-limiter` 레포가 가져가면 안 되는 것

- 인증 principal 생성
- 정책 엔진 평가
- 감사 저장
- 파일 저장

## `oss-contract`에서 참조해야 하는 문서

- `registry/layer1-status.md`
- `registry/layer1-gradle-properties.md`
- `registry/layer1-ci-cd.md`
- `registry/layer1-maven-central.md`
- `registry/layer1-checklist.md`
- `registry/layer2-status.md`
- `CONTRACT_SYNC.md`

## rate-limiter 레포에서 확인할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/redis-strategy.md`
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

1. 제한 기준과 저장 전략을 분리한다.
2. in-memory와 Redis 책임을 분리한다.
3. `gradle.properties`와 `publish.yml` 구조를 `oss-contract` 표준과 맞춘다.
4. 인증, 정책, 감사, 파일 저장 책임과 섞이지 않게 한다.
5. public 계약과 내부 구현을 분리한다.

## 문구 기준

- `rate-limiter`는 요청 속도 제한 라이브러리다.
- `rate-limiter`는 요청 진입 보호의 일부다.
- `rate-limiter`는 IP / 사용자 ID / API 키 기준 제한을 책임진다.
- `rate-limiter`는 인증 principal, 정책 평가, 감사 저장을 책임지지 않는다.

## 체크리스트

- [ ] 제한 기준이 명확한가
- [ ] in-memory와 Redis 책임이 분리되는가
- [ ] Spring 연동이 분리되어 있는가
- [ ] `gradle.properties`와 `publish.yml`이 표준 구조를 따르는가
- [ ] platform 책임과 구현 책임이 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

## 동기화 기록

- 마지막 동기화 일자:
- 반영 요약:
- 남은 작업:
