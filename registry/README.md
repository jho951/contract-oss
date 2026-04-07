# SOT Registry

이 레포는 구현 코드를 담지 않고, 계층 경계와 계약만 관리한다.

## Core Docs

- [layer1-status.md](layer1-status.md): 1계층 현황과 운영 절차
- [layer1-gradle-properties.md](layer1-gradle-properties.md): 1계층 gradle.properties 표준
- [layer1-ci-cd.md](layer1-ci-cd.md): 1계층 CI/CD 표준
- [layer1-maven-central.md](layer1-maven-central.md): 1계층 Maven Central 구조 표준
- [layer1-checklist.md](layer1-checklist.md): 1계층 공통 점검표
- [layer2-status.md](layer2-status.md): 2계층 현황과 운영 절차

## Catalog

- [repositories/README.md](../repositories/README.md): 레포 카탈로그 진입점
- [repositories/layer1.md](../repositories/layer1.md): 1계층 OSS 묶음
- [repositories/layer2.md](../repositories/layer2.md): 2계층 platform 묶음

## Rules

- 1계층 레포 문서에는 계층 매핑을 반복하지 않는다.
- 1계층 OSS는 기능별 책임과 published artifact 경계만 가진다.
- platform 레포는 1계층 published artifact의 exact version만 pin 한다.
- public 문서는 역할과 경계를, registry는 SOT와 규칙을 담는다.
