# 2계층 공통 점검표

이 문서는 기준을 다시 정의하지 않는다.
각 항목은 기준 소유 문서가 적용됐는지만 확인한다.

## 구조 점검

- [ ] `README.md`가 있다.
- [ ] `build.gradle` 구조는 [build-gradle.md](build-gradle.md)를 따른다.
- [ ] `settings.gradle` 구조는 [settings-gradle.md](settings-gradle.md)를 따른다.
- [ ] CI/CD 구조는 [ci-cd.md](ci-cd.md)를 따른다.
- [ ] docs 구조는 [docs-structure.md](docs-structure.md)를 따른다.

## 제거 점검

- [ ] `CONTRACT_SYNC.md`가 없다.
- [ ] `.DS_Store`가 없다.
- [ ] `.gradle/`이 없다.
- [ ] `.idea/`가 없다.
- [ ] `build/`가 없다.
- [ ] 레포 루트에 생성 산출물이 없다.

## 의존성 점검

- [ ] 의존성 기준은 [build-gradle.md](build-gradle.md)를 따른다.
- [ ] local layer1 substitution 기준은 [settings-gradle.md](settings-gradle.md)를 따른다.

## 모듈 점검

- [ ] module 선언 기준은 [settings-gradle.md](settings-gradle.md)를 따른다.
- [ ] build module 책임 분리는 [build-gradle.md](build-gradle.md)를 따른다.

## 책임 점검

- [ ] 공통 책임 경계는 [README.md](README.md)를 따른다.
- [ ] platform별 책임 경계는 해당 platform 표준 문서를 따른다.

## 레포별 특화 점검

- [ ] `platform-security`는 [platform-security-standard.md](platform-security-standard.md)를 따른다.
- [ ] `platform-integrations`는 [platform-integrations-standard.md](platform-integrations-standard.md)를 따른다.
- [ ] 나머지 platform별 현재 상태는 [../../repositories/layer2/README.md](../../repositories/layer2/README.md)에 기록한다.
