# SOT Registry

`registry`는 계층 기준과 운영 규칙의 중앙 기준이다.

## 1계층

- [layer1/README.md](layer1/README.md): 1계층 OSS 기준과 운영 절차
- [layer1/properties-standard.md](layer1/properties-standard.md): 1계층 gradle.properties 표준과 템플릿
- [layer1/build-gradle.md](layer1/build-gradle.md): 1계층 build.gradle 구조 기준
- [layer1/settings-gradle.md](layer1/settings-gradle.md): 1계층 settings.gradle 구조 기준
- [layer1/ci-cd.md](layer1/ci-cd.md): 1계층 CI/CD와 publish.yml 구조 기준
- [layer1/maven-central.md](layer1/maven-central.md): 1계층 Maven Central 구조 표준
- [layer1/repository-readme.md](layer1/repository-readme.md): 1계층 README 구조 기준
- [layer1/docs-structure.md](layer1/docs-structure.md): 1계층 docs 구조 기준
- [layer1/checklist.md](layer1/checklist.md): 1계층 공통 점검표

## 2계층

- [layer2/README.md](layer2/README.md): 2계층 platform 기준과 운영 절차
- [layer2/build-gradle.md](layer2/build-gradle.md): 2계층 build.gradle 구조 기준
- [layer2/settings-gradle.md](layer2/settings-gradle.md): 2계층 settings.gradle 구조 기준
- [layer2/ci-cd.md](layer2/ci-cd.md): 2계층 CI/CD와 publish 구조 기준
- [layer2/docs-structure.md](layer2/docs-structure.md): 2계층 docs 구조 기준
- [layer2/checklist.md](layer2/checklist.md): 2계층 공통 점검표
- [layer2/platform-security-standard.md](layer2/platform-security-standard.md): platform-security 표준 구조와 경계 규칙

## 카탈로그

- [repositories/README.md](../repositories/README.md): 레포 카탈로그 진입점
- [repositories/layer1/README.md](../repositories/layer1/README.md): 1계층 OSS 묶음
- [repositories/layer2/README.md](../repositories/layer2/README.md): 2계층 platform 묶음

## 규칙

- 1계층 레포 문서에는 계층 매핑을 반복하지 않는다.
- 1계층 OSS는 순수 기능 모듈의 본질, 규칙, 계약만 가진다.
- 2계층 platform은 서비스가 붙는 조립 계층이다.
- 3계층 application은 실제 애플리케이션이라는 개념이다.
- public 문서는 역할과 경계를, registry는 SOT와 규칙을 담는다.
