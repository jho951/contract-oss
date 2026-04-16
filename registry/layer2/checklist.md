# 2계층 공통 점검표

## 구조 점검

- [ ] `README.md`가 있다.
- [ ] `build.gradle`이 있다.
- [ ] `settings.gradle`이 있다.
- [ ] `gradle/`, `gradlew`, `gradlew.bat`이 있다.
- [ ] `.github/workflows/build.yml`이 있다.
- [ ] `.github/workflows/publish.yml`이 있다.
- [ ] `docs/README.md`가 있다.
- [ ] `docs/architecture.md`가 있다.
- [ ] `docs/modules.md`가 있다.
- [ ] `docs/extension-guide.md`가 있다.

## 제거 점검

- [ ] `CONTRACT_SYNC.md`가 없다.
- [ ] `.DS_Store`가 없다.
- [ ] `.gradle/`이 없다.
- [ ] `.idea/`가 없다.
- [ ] `build/`가 없다.
- [ ] 레포 루트에 생성 산출물이 없다.

## 의존성 점검

- [ ] 1계층 OSS 의존성은 exact version으로 pin되어 있다.
- [ ] dynamic version, version range, `latest.release`, `+` 참조가 없다.
- [ ] local layer1 substitution은 명시적 option으로만 활성화된다.
- [ ] 기본 build는 published artifact 기준으로 동작한다.

## 모듈 점검

- [ ] `settings.gradle` module 목록이 README / docs와 일치한다.
- [ ] BOM, API/SPI, core, adapter, autoconfigure, starter 역할이 섞이지 않는다.
- [ ] sample consumer는 내부 검증용으로 분리되어 있다.
- [ ] test support는 production 공개 표면과 분리되어 있다.

## 책임 점검

- [ ] 1계층 내부 구현을 재정의하지 않는다.
- [ ] 서비스 비즈니스 로직을 포함하지 않는다.
- [ ] 도메인 권한 판단을 포함하지 않는다.
- [ ] 3계층 application이 소비할 integration API가 분명하다.

## 레포별 특화 점검

- [ ] `platform-security`: 역할별 starter와 security pipeline 경계가 명확하다.
- [ ] `platform-governance`: audit/config/engine 조립 경계가 명확하다.
- [ ] `platform-resource`: resource owner/kind/catalog/lifecycle 경계가 명확하다.
