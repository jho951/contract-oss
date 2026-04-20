# notification Standard

이 문서는 `notification` 1계층 OSS의 표준 책임과 경계를 고정한다.

## 목적

- 알림 메시지 모델과 전달 인터페이스를 제공한다.
- 전달 채널 조합과 framework-independent primitive를 순수 기능으로 유지한다.
- 2계층 `platform-resource`나 다른 platform이 lifecycle 부수효과에 notification primitive를 조립할 수 있게 한다.

## 계층 원칙

- `notification`은 1계층 OSS다.
- `notification`은 message와 delivery primitive를 제공한다.
- resource lifecycle, audit, 정책 위반 대응 같은 platform-level orchestration은 1계층 책임이 아니다.
- 특정 서비스의 알림 문구, 수신자 정책, 업무 이벤트 의미는 소비자 또는 platform 책임이다.

## 모듈 기준

- `notification-api`
- `notification-core`

## 포함해야 할 것

- notification message 모델
- recipient / channel 모델
- dispatcher 계약
- delivery result 모델
- channel adapter 확장 지점
- framework-independent 기본 구현

## 포함하지 말아야 할 것

- resource lifecycle orchestration
- 서비스별 알림 taxonomy hardcoding
- audit 기록
- policy violation handling
- Spring Boot starter 조립

## 판정 기준

- 메시지를 어떤 채널로 전달하는 primitive면 `notification` 책임이다.
- 어떤 resource lifecycle이나 도메인 사건에서 알림을 발생시킬지 정하면 platform 또는 소비자 서비스 책임이다.
