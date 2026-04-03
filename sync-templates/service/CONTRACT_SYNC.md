# CONTRACT_SYNC - service

이 문서는 실제 서비스 레포를 `service-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `service-contract`
- 대상 레포: 실제 서비스 서버
- 대상 역할: 고객/업무 기능 구현

## 실제 서비스가 가져가야 하는 것

- 주문, 예약, 정산 같은 비즈니스 흐름
- platform-security 조립
- platform-governance 조립
- platform-storage 조립
- 서비스 고유 API

## 실제 서비스가 가져가면 안 되는 것

- platform 내부 구현
- 1계층 OSS 구현 세부사항
- 공통 계약의 재정의
- 서비스가 아닌 플랫폼 역할

## 동기화 절차

1. 서비스의 API와 흐름을 `service-contract`에 맞춘다.
2. 필요한 플랫폼 기능만 조립해서 쓴다.
3. 플랫폼의 내부 구현을 복제하지 않는다.
4. 서비스별 문서를 `service-contract`와 일치시킨다.

## 문구 기준

- 서비스는 고객/업무 기능을 구현한다.
- 서비스는 platform을 조립해서 쓴다.
- 서비스는 계약을 구현하는 최상단이다.

## 체크리스트

- [ ] 서비스 고유 API가 보이는가
- [ ] platform 조립 구조가 드러나는가
- [ ] platform 내부 구현을 침범하지 않는가
- [ ] `service-contract`와 문구가 맞는가

