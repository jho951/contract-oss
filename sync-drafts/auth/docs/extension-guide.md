# Extension Guide

이 문서는 `auth`를 확장할 때 따라야 할 규칙을 정리한다.

## 추가 가능 범위

- 새로운 token strategy
- 새로운 principal resolver
- 새로운 session store
- 새로운 Spring integration

## 추가 불가 범위

- 정책 엔진 구현
- 감사 저장 구현
- 파일 저장 구현
- 서비스 고유 비즈니스 규칙

## 확장 규칙

1. 공통 인터페이스를 먼저 정의한다.
2. 구현은 별도 모듈로 추가한다.
3. service-contract와 충돌하지 않게 한다.
4. oss-contract의 용어를 유지한다.

