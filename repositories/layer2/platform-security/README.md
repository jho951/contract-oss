# platform-security

## 목표 역할

- 인증과 인가 실행 플랫폼
- 토큰, 세션, 인증 필터, 권한 진입점 표준화

## 위치

- 이 문서는 현재 조직 표준 security line으로 운영하는 `platform-security`를 설명한다.
- 같은 1계층 OSS (`auth`, `ip-guard`, `rate-limiter`)를 바탕으로 다른 security 2계층 line을 만드는 것은 가능하다.
- 아래 starter와 add-on은 `platform-security` line의 published surface이지, 1계층을 `platform-security`에 영구 고정한다는 뜻은 아니다.

## 현재 main 반영 포인트

- 기본 소비 진입점은 현재 `platform-security` line에서 `platform-security-starter`다.
- sanctioned bridge는 `platform-security-auth-bridge-starter`, `platform-security-ratelimit-bridge-starter`다.
- sanctioned adapter는 `platform-security-hybrid-web-adapter`다.
- 서비스 간 outbound 보안 전파는 `platform-security-client`를 공식 add-on으로 사용한다.
- sample consumer는 서비스가 직접 header/interceptor glue를 만들지 않아도 되는 경로를 검증한다.

## 주로 소비하는 OSS

- `auth`
- `ip-guard`
- `rate-limiter`

## 플랫폼이 소유해야 할 것

- 인증 필터 체인
- 로그인 파이프라인
- JWT 발급과 검증
- refresh token 정책
- logout 처리
- SecurityContext 구성
- 인증 실패 응답 표준화
- 인증 이벤트 발행
- 권한 검증 진입점
- IP guard와 rate limit 집행

## 서비스가 해야 하는 것

- 사용자 조회
- credential 저장소 연결
- refresh token 저장소 구현
- 서비스별 설정 선언

## 서비스가 하지 말아야 하는 것

- 직접 JWT 발급
- 직접 인증 필터 구현
- 직접 보안 실패 응답 포맷 구현
- raw auth OSS를 서비스 contract처럼 노출

## 검증 기준

- publish surface에 `client`, sanctioned bridge starter, sanctioned adapter가 모두 포함돼야 한다.
- `verifyPublishedSurface`, `verifyStarterContract`, `verifyConsumerConformance`, `verifyStage5Contract`를 기본 gate로 본다.

## 의존 방향

- `platform-security -> platform-governance`는 가능하다.
- 반대로 `platform-governance -> platform-security` 순환 의존은 금지한다.
