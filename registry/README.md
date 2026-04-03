# SOT Registry

이 레포는 직접 구현 코드를 담지 않는다.

역할은 다음 3가지를 하나의 진실원천으로 관리하는 것이다.

- 현재 존재하는 1계층 OSS 레포들
- 앞으로 만들 2계층 platform 구조
- 앞으로 만들어질 3계층 service 구조
- 계층 사이의 소유권, 의존성, 경계 규칙

## 관리 대상

- 현재 OSS: [current-oss.md](current-oss.md)
- 확인된 역할: [observed-roles.md](observed-roles.md)
- 미래 platform: [future-platforms.md](future-platforms.md)
- 미래 service: [service-layer.md](service-layer.md)
- 서비스 기준 계약: [service-contract.md](service-contract.md)
- 실행 순서: [release-execution-order.md](release-execution-order.md)

## 관리 내용

- 어떤 OSS가 어떤 플랫폼으로 흡수되는지
- 어떤 계약이 공통인지
- 어떤 레포가 어떤 책임을 가지는지
- 플랫폼끼리 직접 얽히지 않도록 하는 규칙
- 실제 레포에 반영하는 커밋 / push / tag 순서
