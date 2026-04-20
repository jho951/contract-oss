# build.gradle 구조 기준 - 2계층 Platform

2계층 platform의 `build.gradle`은 내부 platform package를 조립하고 배포하는 구조를 기준으로 한다.

## 기본 원칙

- 1계층 OSS published artifact를 exact version으로 소비한다.
- dynamic version, version range, `latest.release`, `+` 참조는 금지한다.
- 1계층 내부 구현을 2계층에서 재정의하지 않는다.
- platform module은 responsibility first로 나눈다.
- sample consumer나 test support는 production 공개 표면과 구분한다.
- platform 간 bridge module은 본체 platform 내부 module을 직접 참조하지 않고 published platform API artifact를 소비한다.

## 공통 plugin 기준

2계층 레포는 Java/Gradle multi-module 구조를 전제로 한다.
실제 plugin 구성은 platform 배포 방식에 맞추되, 아래 책임을 분리한다.

- Java library module
- BOM module
- Spring integration module
- Spring Boot starter / autoconfigure module
- test support module
- sample consumer module

## 의존성 기준

- 1계층 의존성은 platform BOM 또는 version catalog를 통해 pin한다.
- 1계층 의존성 버전은 `repositories/layer1/README.md`의 기준 버전과 충돌하지 않아야 한다.
- 로컬 검증용 composite build는 선택 옵션으로만 둔다.
- production build는 Maven Central 또는 내부 package에 배포된 artifact를 기준으로 한다.
- `platform-integrations`는 연결 대상 platform 버전을 exact version으로 pin하고, bridge artifact version은 자체 release version으로 관리한다.

## 금지

- 1계층 source set 직접 복사
- 1계층 내부 구현 재정의
- 소비자 비즈니스 로직 추가
- 도메인 권한 판단 추가
- bridge module에서 본체 platform의 내부 구현 class 직접 사용
- 생성 산출물 포함
