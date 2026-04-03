# Modules

이 저장소의 모듈은 IP 접근 제어 책임을 분리해서 담는다.

## 모듈 역할

- `ip-guard-core`: IP 판단 규칙
- `ip-guard-spring`: Spring 어댑터
- `ip-guard-spring-boot-starter`: 자동 설정 진입점

## 모듈 원칙

- 핵심 판단은 core에 둔다.
- Spring 종속성은 adapter와 starter로 격리한다.
- 테스트 유틸은 production path에 넣지 않는다.

