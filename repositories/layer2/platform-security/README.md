# platform-security

## 목표 역할

- 인증과 인가 실행 플랫폼
- 토큰, 세션, 인증 필터, 권한 진입점 표준화

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

## 의존 방향

- `platform-security -> platform-governance`는 가능하다.
- 반대로 `platform-governance -> platform-security` 순환 의존은 금지한다.
