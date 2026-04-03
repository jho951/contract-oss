# Extension Guide

이 문서는 `service-contract`를 확장할 때 따라야 할 규칙을 정리한다.

## 추가 가능 범위

- 새로운 service API
- 새로운 inter-service contract
- 새로운 env key
- 새로운 OpenAPI schema

## 추가 불가 범위

- platform 내부 구현
- OSS 내부 구현
- 서비스 구현 코드

## 확장 규칙

1. 서비스 외부 약속을 먼저 정의한다.
2. 구현이 아닌 계약만 추가한다.
3. 플랫폼과 충돌하지 않게 한다.
4. 버전 호환 규칙을 명시한다.

