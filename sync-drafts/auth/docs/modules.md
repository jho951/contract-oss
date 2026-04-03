# Modules

이 저장소의 모듈은 인증 책임을 분리해서 담는다.

## 모듈 역할

- `auth-core`: 핵심 인증 모델, 인터페이스, 공통 규칙
- `auth-jwt`: JWT token 발급/검증
- `auth-session`: 세션 저장/조회
- `auth-hybrid`: 인증 전략 조합
- `auth-spring`: Spring 어댑터
- `auth-spring-boot-starter`: 자동 설정 진입점
- `auth-common-test`: 테스트 지원

## 모듈 원칙

- 핵심 규칙은 `auth-core`에 둔다.
- 구현은 전략별 모듈로 나눈다.
- Spring 종속성은 어댑터와 starter로 격리한다.
- 테스트 유틸은 production path에 넣지 않는다.

