# Extension Guide

이 문서는 `audit-log`를 확장할 때 따라야 할 규칙을 정리한다.

## 추가 가능 범위

- 새로운 sink
- 새로운 masking rule
- 새로운 event enrichment
- 새로운 Spring integration

## 추가 불가 범위

- 인증 token 발급
- 정책 엔진 평가
- 파일 저장 구현
- 서비스 비즈니스 규칙

## 확장 규칙

1. 공통 이벤트 구조를 먼저 정의한다.
2. 구현은 별도 sink/adapter 모듈로 추가한다.
3. service-contract와 충돌하지 않게 한다.
4. oss-contract의 용어를 유지한다.

