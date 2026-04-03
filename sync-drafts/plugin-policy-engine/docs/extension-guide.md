# Extension Guide

이 문서는 `plugin-policy-engine`를 확장할 때 따라야 할 규칙을 정리한다.

## 추가 가능 범위

- 새로운 evaluation strategy
- 새로운 rollout rule
- 새로운 targeting rule
- 새로운 variant rule

## 추가 불가 범위

- 정책 키 조회
- 감사 저장 구현
- 인증 token 처리
- 파일 저장 구현

## 확장 규칙

1. 공통 평가 인터페이스를 먼저 정의한다.
2. 구현은 별도 strategy 모듈로 추가한다.
3. service-contract와 충돌하지 않게 한다.
4. oss-contract의 용어를 유지한다.

