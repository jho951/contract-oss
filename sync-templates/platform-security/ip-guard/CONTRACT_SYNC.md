# CONTRACT_SYNC - ip-guard

이 문서는 `ip-guard` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `ip-guard`
- 대상 역할: IP 허용/차단, 요청 진입 제어, core 판단 로직, Spring 연동

## `ip-guard` 레포가 가져가야 하는 것

- IP 허용/차단
- 요청 진입 제어
- core 판단 로직
- Spring 연동

## `ip-guard` 레포가 가져가면 안 되는 것

- 인증 token 발급
- principal 생성
- 정책 저장
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

## ip-guard 레포에서 확인할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/access-flow.md`
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

1. IP 판단과 요청 진입 제어 책임을 명확히 한다.
2. Spring 연동과 core 판단 로직을 분리한다.
3. `gradle.properties`와 `publish.yml` 구조를 `oss-contract` 표준과 맞춘다.
4. 인증, 정책, 감사, 파일 저장 책임과 섞이지 않게 한다.
5. public 계약과 내부 구현을 분리한다.

## 문구 기준

- `ip-guard`는 IP 접근 제어 구현 레포다.
- `ip-guard`는 요청 진입 보안의 일부다.
- `ip-guard`는 접근 허용/차단과 core 판단을 책임진다.
- `ip-guard`는 인증 token, 정책 평가, 감사 저장을 책임지지 않는다.

## 체크리스트

- [ ] IP 판단 책임이 명확한가
- [ ] 요청 진입 제어가 분리되어 있는가
- [ ] Spring 연동이 별도 문서로 정리되는가
- [ ] `gradle.properties`와 `publish.yml`이 표준 구조를 따르는가
- [ ] platform 책임과 구현 책임이 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

## 동기화 기록

- 마지막 동기화 일자:
- 반영 요약:
- 남은 작업:
