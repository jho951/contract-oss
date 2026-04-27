# platform-governance

## 목표 역할

- 감사와 정책과 운영 통제 플랫폼
- audit, policy config, policy engine, violation handling 표준화

## 주로 소비하는 OSS

- `audit-log`
- `policy-config`
- `plugin-policy-engine`

## 플랫폼이 소유해야 할 것

- audit event 표준 모델
- audit sink 표준화
- policy config loading
- plugin policy engine 실행
- 운영 정책 평가 결과 표준화
- violation handler
- 운영 기본값과 fail-fast 기준

## 서비스가 해야 하는 것

- 어떤 행위를 감사 대상으로 볼지 선언
- 어떤 use case에 정책을 붙일지 선언
- audit context 제공

## 서비스가 하지 말아야 하는 것

- 직접 audit 포맷 정의
- 직접 정책 엔진 호출 흐름 재구현
- 직접 운영 판단 모델 정의

## 의존 방향

- `platform-governance`는 정책과 감사 기준의 owner다.
- 인증 집행은 `platform-security`, 리소스 lifecycle은 `platform-resource`, outbound 전달은 `platform-integrations`가 owner다.
