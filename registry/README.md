# Registry

## 역할

- 계층 기준과 운영 규칙의 중앙 기준입니다.

## 경계

- 1계층 레포 문서에는 계층 매핑을 반복하지 않는다.
- 1계층 OSS는 순수 기능 모듈의 본질, 규칙, 계약만 가진다.
- 2계층 platform은 서비스가 붙는 조립 계층이다.
- public 문서는 역할과 경계를, registry는 SOT와 규칙을 담는다.

## 문서
- [layer1/README.md](layer1/README.md): 1계층 OSS 기준과 운영 절차
- [layer2/README.md](layer2/README.md): 2계층 platform 기준과 운영 절차
- Layer1 레포별 책임 표준은 `registry/layer1/standards/`가 소유한다.
- Layer2 platform별 책임 표준은 `registry/layer2/standards/`가 소유한다.
- build, settings, Gradle properties 기준은 각 계층의 `structure/`가 소유한다.
- CI/CD, publish, checklist 기준은 각 계층의 `operations/`가 소유한다.
