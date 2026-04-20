# 2계층 공통 점검표

이 문서는 기준을 다시 정의하지 않는다.
각 항목은 기준 소유 문서가 적용됐는지만 확인한다.

## 구조 점검

- [ ] `README.md`가 있다.
- [ ] `gradle.properties` 구조는 [gradle-properties.md](../structure/gradle-properties.md)를 따른다.
- [ ] `build.gradle` 구조는 [build-gradle.md](../structure/build-gradle.md)를 따른다.
- [ ] `settings.gradle` 구조는 [settings-gradle.md](../structure/settings-gradle.md)를 따른다.
- [ ] README는 공개 좌표, 흡수 대상, 제공 module, 책임 경계를 명시한다.
- [ ] CI/CD 구조는 [ci-cd.md](ci-cd.md)를 따른다.
- [ ] docs는 platform 소비와 확장에 필요한 문서만 둔다.

## 제거 점검

- [ ] 내부 계약 동기화 문서가 없다.
- [ ] `.DS_Store`가 없다.
- [ ] Gradle 캐시 디렉터리가 없다.
- [ ] IDE 설정 디렉터리가 없다.
- [ ] 생성 산출물 디렉터리가 없다.
- [ ] 레포 루트에 생성 산출물이 없다.

## 의존성 점검

- [ ] version key 기준은 [gradle-properties.md](../structure/gradle-properties.md)를 따른다.
- [ ] 의존성 기준은 [build-gradle.md](../structure/build-gradle.md)를 따른다.
- [ ] local layer1 substitution 기준은 [settings-gradle.md](../structure/settings-gradle.md)를 따른다.

## publish 점검

- [ ] publish 기준은 [publish.md](publish.md)를 따른다.
- [ ] publish credential은 build workflow에 요구되지 않는다.
- [ ] publish version은 tag 또는 release input에서 주입된다.

## 모듈 점검

- [ ] module 선언 기준은 [settings-gradle.md](../structure/settings-gradle.md)를 따른다.
- [ ] build module 책임 분리는 [build-gradle.md](../structure/build-gradle.md)를 따른다.

## 책임 점검

- [ ] 공통 책임 경계는 [README.md](../README.md)를 따른다.
- [ ] platform별 책임 경계는 해당 platform 표준 문서를 따른다.

## 레포별 특화 점검

- [ ] `platform-security`는 [platform-security.md](../standards/platform-security.md)를 따른다.
- [ ] `platform-governance`는 [platform-governance.md](../standards/platform-governance.md)를 따른다.
- [ ] `platform-resource`는 [platform-resource.md](../standards/platform-resource.md)를 따른다.
- [ ] `platform-integrations`는 [platform-integrations.md](../standards/platform-integrations.md)를 따른다.
- [ ] platform별 현재 상태는 [../../../repositories/layer2/README.md](../../../repositories/layer2/README.md)에 기록한다.
