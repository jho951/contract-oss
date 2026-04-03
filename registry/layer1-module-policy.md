# 1계층 모듈 정책

이 문서는 1계층 OSS 전체에 적용할 모듈 정책을 정리한다.

## 기본 정책

- 모든 1계층 OSS는 멀티모듈을 기본값으로 본다.
- 단순한 레포도 필요하면 core/spring/starter 패턴을 따른다.
- `auth`가 기준 레포다.
- 나머지 레포는 `auth`의 모듈 명명 규칙을 최대한 따른다.

## 권장 분리 기준

### core

- 순수 도메인 규칙
- SPI 인터페이스
- 구현 독립 모델

### api

- 외부가 직접 의존해야 하는 계약
- 구현과 분리되어야 하는 인터페이스

### spring

- Spring annotation / bean / configuration binding

### autoconfigure

- Spring Boot 자동 구성
- starter와 분리할 필요가 있을 때만 사용

### starter

- 애플리케이션에서 가장 먼저 가져가는 진입점

### common-test

- 테스트 픽스처
- in-memory 구현
- 샘플/통합 테스트 지원

## 금지 정책

- core에 Spring 의존성을 넣지 않는다.
- starter에 도메인 구현을 넣지 않는다.
- api에 구현 세부사항을 넣지 않는다.
- common-test를 production 모듈에 섞지 않는다.

