# service-contract

## 계층

- 3계층 계약 기준

## 상태

- 계획/기준 저장소

## 소유 기준

- `sync-final/service-contract/CONTRACT_SYNC.md`
- `registry/service-layer.md`

## 책임

- 서비스 요청/응답 스펙
- 서비스 간 인터페이스
- env 규격
- OpenAPI 규약
- 공통 에러 코드

## 현재

- 서비스 서버용 계약 기준만 정의
- platform 계약과 분리

## 목표

- 모든 실제 서비스 서버가 따르는 3계층 계약 기준
- 서비스 문서와 플랫폼 문서의 경계 고정

## 변경 포인트

- 서비스 요청/응답
- env
- OpenAPI
- error code
- 호환 규칙

## 관계

- `oss-contract`와 목적이 다르다.
- 실제 서비스 서버는 이 기준을 따른다.

## 기준 문서

- [sync-final/service-contract/CONTRACT_SYNC.md](../sync-final/service-contract/CONTRACT_SYNC.md)
