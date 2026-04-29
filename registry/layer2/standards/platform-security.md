# platform-security Standard

이 문서는 `platform-security`가 L5 목표 구조에서 어떤 책임을 가져야 하는지 고정한다.

## 적용 범위

- 이 문서는 현재 조직이 운영하는 security 2계층 line으로서의 `platform-security` 기준을 정의한다.
- 이것이 2계층 security platform의 유일한 형태라는 뜻은 아니다.
- 다른 팀이나 프로젝트도 같은 1계층 OSS (`auth`, `ip-guard`, `rate-limiter`)를 사용해 다른 security 2계층 line을 만들 수 있다.
- 다만 서비스 하나는 raw OSS 대신 자신이 선택한 security platform line의 contract를 소비해야 한다.

## 역할

- 인증과 인가 실행 플랫폼
- 토큰, 세션, 인증 필터, 권한 진입점의 표준 실행 계층
- ingress에서 실제로 보안을 집행하는 계층

## 목적

- `auth`, `ip-guard`, `rate-limiter` OSS를 서비스마다 따로 조립하지 않게 한다.
- 인증과 인가 실행 흐름을 현재 조직 표준 방식으로 제공한다.
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

## 현재 main 기준 public surface

- `platform-security-starter`를 현재 `platform-security` line의 기본 진입점으로 둔다.
- `platform-security-auth-bridge-starter`는 auth OSS와 platform contract를 연결하는 공식 bridge다.
- `platform-security-ratelimit-bridge-starter`는 rate-limit 집행과 platform contract를 연결하는 공식 bridge다.
- `platform-security-hybrid-web-adapter`는 web/security 조합 진입점을 제공하는 sanctioned adapter다.
- `platform-security-client`는 서비스 간 보안 header propagation을 위한 공식 add-on이다.
- sample consumer는 서비스가 직접 interceptor나 header glue를 재구현하지 않아도 되는 경로를 검증해야 한다.

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

## 검증 기준

- `verifyPublishedSurface`는 publish 대상에 `client`, sanctioned bridge starter, sanctioned adapter가 빠지지 않았는지 확인해야 한다.
- `verifyStarterContract`는 서비스가 starter 하나로 필요한 기본 보안 조립을 가져갈 수 있는지 확인해야 한다.
- `verifyConsumerConformance`는 sample consumer가 raw OSS 없이 platform contract만으로 동작하는지 확인해야 한다.
- `verifyStage5Contract`는 public surface에 1계층 타입이 새지 않았는지 확인해야 한다.

## 운영 프로필과 fail-fast 기준

- production profile 기본값은 `["prod", "production"]`를 사용한다.
- `EDGE`, `API_SERVER`, `INTERNAL_SERVICE`, `ISSUER`는 같은 규칙으로 뭉개지지 않고 preset별로 다르게 판정한다.
- 운영 예외는 명시적 opt-out으로만 허용한다.
