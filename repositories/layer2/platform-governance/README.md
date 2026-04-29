# platform-governance

## 목표 역할

- 감사와 정책과 운영 통제 플랫폼
- audit, policy config, policy engine, violation handling 표준화

## 위치

- 이 문서는 현재 조직 표준 governance line으로 운영하는 `platform-governance`를 설명한다.
- 같은 1계층 OSS (`audit-log`, `policy-config`, `plugin-policy-engine`)를 바탕으로 다른 governance 2계층 line을 만드는 것은 가능하다.
- 아래 starter와 SPI는 `platform-governance` line의 published surface이지, 1계층을 `platform-governance`에 영구 고정한다는 뜻은 아니다.

## 현재 main 반영 포인트

- 공식 public SPI는 `GovernanceAuditSink`, `GovernanceAuditRecorder`, `PolicyConfigSource`, `GovernanceDecisionEngine`, `ViolationHandler`다.
- `ViolationHandler`는 확장 포인트로 검증되고, sample/smoke 경로에서 public contract로 취급한다.
- local source 검증은 `./gradlew check -PuseLocalLayer1=true` 경로를 유지한다.
- dependency locking 완화는 local source 검증 모드에서만 허용한다.

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

## 검증 기준

- governance starter와 public SPI가 publish surface에 포함돼야 한다.
- `verifyPublishedSurface`, `verifyStarterContract`, `verifyConsumerConformance`, `verifyStage5Contract`를 기본 gate로 본다.

## 의존 방향

- `platform-governance`는 정책과 감사 기준의 owner다.
- 인증 집행은 `platform-security`, 리소스 lifecycle은 `platform-resource`, outbound 전달은 `platform-integrations`가 owner다.
