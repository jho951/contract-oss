# Extension Guide

이 문서는 `file-storage-module`을 확장할 때 따라야 할 규칙을 정리한다.

## 추가 가능 범위

- 새로운 storage backend
- 새로운 path rule
- 새로운 metadata handler
- 새로운 Spring integration

## 추가 불가 범위

- 인증 token 처리
- 정책 엔진 평가
- 감사 저장 구현
- 서비스 비즈니스 규칙

## 확장 규칙

1. 공통 저장 인터페이스를 먼저 정의한다.
2. 구현은 별도 adapter 모듈로 추가한다.
3. service-contract와 충돌하지 않게 한다.
4. oss-contract의 용어를 유지한다.

