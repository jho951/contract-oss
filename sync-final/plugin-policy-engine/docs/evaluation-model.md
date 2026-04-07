# Evaluation Model

`plugin-policy-engine`는 rollout, targeting, variant 선택을 조합해서 정책을 평가한다.

## 흐름

1. 입력 정책과 컨텍스트를 수집한다.
2. rollout 조건을 평가한다.
3. targeting 조건을 평가한다.
4. variant를 선택한다.
5. Spring 연동 계층에 결과를 전달한다.

## 원칙

- 정책 평가는 설정 조회와 분리한다.
- evaluation은 결과를 계산하고, source lookup은 다른 레이어가 담당한다.
- 정책 조합은 core에서 결정하고 프레임워크 종속은 밖으로 둔다.

## 제외 범위

- 정책 키 조회
- 감사 저장
- 인증 token
- 파일 저장
