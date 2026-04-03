# Extension Guide

이 문서는 `policy-config`를 확장할 때 따라야 할 규칙을 정리한다.

## 추가 가능 범위

- 새로운 settings source
- 새로운 key resolver
- 새로운 type conversion
- 새로운 Spring integration

## 추가 불가 범위

- 정책 엔진 평가
- 감사 저장 구현
- 인증 token 처리
- 파일 저장 구현

## 확장 규칙

1. 공통 키/조회 규칙을 먼저 정의한다.
2. 구현은 별도 source/adapter 모듈로 추가한다.
3. service-contract와 충돌하지 않게 한다.
4. oss-contract의 용어를 유지한다.

