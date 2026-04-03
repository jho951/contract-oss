# CONTRACT_SYNC - service-contract

이 문서는 `service-contract` 레포를 기준으로 실제 서비스 서버 문서를 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `service-contract`
- 대상 레포: `service-contract`
- 대상 역할: 실제 서비스 서버들의 계약 SOT

## `service-contract`가 가져가야 하는 것

- 서비스 요청/응답 스펙
- 서비스 간 인터페이스
- 서비스별 환경변수 규격
- 서비스별 OpenAPI 규약
- 서비스별 공통 에러 코드
- 서비스 레벨 호환 규칙

## `service-contract`가 가져가면 안 되는 것

- platform-security 내부 구현
- platform-governance 내부 구현
- platform-storage 내부 구현
- 1계층 OSS의 세부 구현
- 서비스 서버의 개별 구현 코드

## `oss-contract`와의 관계

- `oss-contract`는 OSS와 platform 사이의 계약 SOT다.
- `service-contract`는 실제 서비스 서버와 platform 사이의 계약 SOT다.
- 둘은 목적이 다르며 서로 대체하지 않는다.

## 동기화 절차

1. 서비스 서버가 무엇을 외부에 약속하는지 정리한다.
2. 서비스 간 계약과 플랫폼 계약을 분리한다.
3. env, OpenAPI, error code를 고정한다.
4. 구현 레포는 `service-contract`를 거스르지 않게 맞춘다.

## 문구 기준

- `service-contract`는 실제 서비스 서버들의 계약 기준 저장소다.
- `service-contract`는 플랫폼 구현 세부사항을 담지 않는다.
- `service-contract`는 서비스 API와 호환 규칙을 정의한다.

## 체크리스트

- [ ] 서비스 요청/응답이 정의되어 있는가
- [ ] 서비스 간 인터페이스가 정의되어 있는가
- [ ] env/OpenAPI/error code 규격이 있는가
- [ ] platform 내부 구현과 섞이지 않았는가

