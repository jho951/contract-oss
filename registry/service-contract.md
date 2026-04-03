# service-contract

`service-contract`는 실제 서비스 서버들의 기준 계약 저장소다.

## 다루는 것

- 서비스 서버의 공통 인터페이스
- 서비스 간 계약
- 서비스 요청/응답 스펙
- 서비스별 환경변수 규격
- 서비스별 OpenAPI 규약

## 다루지 않는 것

- 플랫폼 내부 구현
- 1계층 OSS의 세부 구현
- 공통 플랫폼의 내부 운영 방식

## 관계

- `oss-contract`는 OSS와 플랫폼을 잇는 계약 SOT다.
- `service-contract`는 실제 서비스 서버를 잇는 계약 SOT다.
- 실제 서비스 서버는 `service-contract`를 기준으로 플랫폼을 조립한다.

