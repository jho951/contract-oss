# Modules

이 저장소의 모듈은 감사 로그 책임을 분리해서 담는다.

## 모듈 역할

- `audit-log-api`: 감사 인터페이스
- `audit-log-core`: 표준 이벤트 모델과 sink
- `audit-log-spring-boot-autoconfigure`: Spring 설정
- `audit-log-spring-boot-starter`: 자동 설정 진입점

## 모듈 원칙

- 표준 이벤트 모델은 core에 둔다.
- Spring 종속성은 adapter와 starter로 격리한다.
- 테스트 유틸은 production path에 넣지 않는다.

