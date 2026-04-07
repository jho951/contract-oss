# Source Resolution

`policy-config`는 설정 소스를 읽고 정책 키를 해석하는 역할을 분리한다.

## 소스 우선순위

1. 환경변수
2. System Properties
3. `.properties`
4. `Map` 기반 입력

## 원칙

- `PolicyKey<T>`는 타입 안전한 조회 단위다.
- 소스 해석과 키 정의는 같은 책임이 아니다.
- Spring 연동은 조회 결과를 소비하는 어댑터다.

## 제외 범위

- 정책 평가
- 감사 저장
- 인증 token
- 파일 저장
