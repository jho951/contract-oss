# Architecture

`policy-config`는 다양한 설정 소스에서 정책 값을 읽어오는 플랫폼 구현 레포다.

## 설계 원칙

- 정책 설정 조회는 플랫폼 책임이다.
- 서비스는 설정 결과를 소비한다.
- 구현은 contract를 재정의하지 않는다.
- Spring wiring은 adapter layer에 둔다.

## 구성 요소

- `policy-config-core`: 정책 키와 조회 규칙
- `policy-config-spring`: Spring 통합
- `policy-config-spring-boot-starter`: 애플리케이션 진입점

## 경계

- 설정 소스 조회는 이 저장소의 책임이다.
- 정책 실행은 이 저장소의 책임이 아니다.
- 감사 저장은 이 저장소의 책임이 아니다.

