# Modules

이 저장소의 모듈은 정책 조회 책임을 분리해서 담는다.

## 모듈 역할

- `policy-config-core`: 정책 키와 조회 규칙
- `policy-config-spring`: Spring 어댑터
- `policy-config-spring-boot-starter`: 자동 설정 진입점

## 모듈 원칙

- 핵심 조회 로직은 core에 둔다.
- Spring 종속성은 adapter와 starter로 격리한다.

