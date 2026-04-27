# platform-security Standard

이 문서는 `platform-security`가 L5 목표 구조에서 어떤 책임을 가져야 하는지 고정한다.

## 역할

- 인증과 인가 실행 플랫폼
- 토큰, 세션, 인증 필터, 권한 진입점의 표준 실행 계층
- ingress에서 실제로 보안을 집행하는 계층

## 목적

- `auth`, `ip-guard`, `rate-limiter` OSS를 서비스마다 따로 조립하지 않게 한다.
- 인증과 인가 실행 흐름을 회사 표준 방식으로 고정한다.
- 서비스가 보안 실행 세부 구현 대신 platform contract만 보도록 만든다.

## 소유해야 할 것

- 인증 필터 체인
- 로그인 파이프라인
- JWT 발급과 검증
- refresh token 정책
- logout 처리
- SecurityContext 구성
- 인증 실패 응답 표준화
- 인증 이벤트 발행
- 권한 검증 진입점
- IP guard와 rate limit의 실제 집행

## 1계층 조립 기준

- `auth`
- `ip-guard`
- `rate-limiter`

## 포함해야 할 것

- platform-owned auth API와 SPI
- token, session, principal runtime view
- gateway, edge, internal service를 위한 표준 보안 진입점
- starter와 sanctioned add-on
- typed properties
- 운영 fail-fast

## 포함하지 말아야 할 것

- 회원가입, 프로필 변경 같은 비즈니스 로직
- 서비스별 로그인 화면
- 서비스별 URL 하드코딩
- 서비스별 Redis key 규칙
- 서비스별 JWT helper
- 서비스별 인증 필터 재구현

## 확장 규칙

- 서비스는 raw OSS 타입을 직접 import하지 않는다.
- platform public surface는 platform-owned 타입으로 닫는다.
- 정책의 owner는 `platform-governance`지만, 요청 흐름에서 차단하고 집행하는 owner는 `platform-security`다.
- 보안 이벤트는 기록할 수 있지만 audit pipeline owner는 `platform-governance`다.

## 운영 프로필과 fail-fast 기준

- production profile 기본값은 `["prod", "production"]`를 사용한다.
- `EDGE`, `API_SERVER`, `INTERNAL_SERVICE`, `ISSUER`는 같은 규칙으로 뭉개지지 않고 preset별로 다르게 판정한다.
- 운영 예외는 명시적 opt-out으로만 허용한다.
