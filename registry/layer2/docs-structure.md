# docs 구조 기준 - 2계층 Platform

2계층 platform의 docs는 platform 소비와 확장에 필요한 문서를 제공한다.
bridge-only repo는 별도 docs 디렉터리 없이 repo `README.md`에 bridge 목적, 소비 의존성, publish 단위를 모아도 된다.

## 공통 목표 구조

```text
docs/
  README.md
  architecture.md
  modules.md
  extension-guide.md
```

platform 책임에 따라 아래 문서를 추가할 수 있다.

- `quickstart.md`
- `configuration.md`
- `usage.md`
- `private-publish.md`
- platform별 모델 문서
- troubleshooting 문서

## 작성 기준

- `README.md`는 문서 지도를 제공한다.
- `architecture.md`는 1계층 조립 흐름과 platform 내부 책임을 설명한다.
- `modules.md`는 실제 `settings.gradle` module과 일치해야 한다.
- `extension-guide.md`는 properties, customizer, override bean, SPI 등 확장 표면을 설명한다.
- private publish 문서는 내부 배포 흐름만 설명한다.

## 금지

- 소비자별 비즈니스 정책 문서화
- 도메인 권한 판단을 platform 책임처럼 설명
- 1계층 OSS 내부 구현 문서 복제
- `oss-contract`의 registry 기준을 장문으로 반복
