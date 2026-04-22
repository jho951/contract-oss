# platform-security Standard

이 문서는 `platform-security` 2계층 platform의 표준 구조와 경계를 고정한다.

## 목적

- `auth`, `ip-guard`, `rate-limiter` 1계층 OSS를 조립하는 표준 2계층을 정의한다.
- 공통 보안 파이프라인을 표준화한다.
- platform 소비자가 쉽게 가져다 쓸 수 있는 내부 비공개 platform 경계를 고정한다.
- 1계층 OSS를 platform 내부 adapter로 흡수하고 소비자에게는 platform 소유 보안 port만 노출한다.

## 계층 원칙

- 1계층 OSS는 공개 배포 가능한 독립 라이브러리로 취급한다.
- 2계층 `platform-security`는 1계층 OSS를 조합하는 내부 비공개 platform layer로 취급한다.
- 2계층은 범용 설계를 유지하되 외부 공개 라이브러리처럼 소비되는 계층이 아니다.
- 2계층의 공개 표면은 내부 소비자 공통 사용을 전제로 한다.
- 확장은 `properties`, `customizer`, `override bean`, 단일 starter, service role preset을 통해 제공한다.
- 현재 소비 진입점은 단일 `platform-security-starter`와 `platform.security.service-role-preset`이다.
- 2계층은 소비자별 비즈니스 로직, 도메인 권한 판단, 회원가입, 로그인 화면, 특정 URL, Redis key 규칙을 포함하지 않는다.
- `policy-config`, audit pipeline, feature flag config 호환 기준의 owner는 `platform-governance`다.
- `platform-security`는 보안 평가와 보안 event/publisher 계약을 소유하고, governance audit 기록 구현은 소유하지 않는다.
- 1계층 `auth`, `rate-limiter` bean 타입을 소비 서비스가 직접 맞춰 노출하도록 요구하지 않는다.
- 공개 auth/rate-limit 계약은 `platform-security-ports`의 platform-owned runtime view와 port로 닫는다.
- `platform-security-adapter-auth`, `platform-security-adapter-ratelimiter`는 raw `com.auth.*`, raw `RateLimiter` 같은 1계층 결합을 흡수하는 adapter 역할로만 둔다.
- platform 내부 auto-configuration과 운영 정책은 platform 소유 port/adapter를 기준으로 판단한다.
- policy, auto-configuration, gateway 통합 표면은 raw auth/rate-limit SPI가 아니라 platform 소유 decision/adapter 계약만 본다.

## 1계층 조립 기준

- `auth`: `auth-core`, `auth-jwt`, `auth-session`, `auth-hybrid`, `auth-apikey`, `auth-hmac`, `auth-oidc`, `auth-service-account`
- `ip-guard`: `ip-guard-core`, `ip-guard-spi`
- `rate-limiter`: `rate-limiter-core`, `rate-limiter-spi`

## platform 소유 경계 기준

- `platform-security`는 1계층 OSS 타입을 직접 public contract처럼 소비자에게 요구하지 않는다.
- token/session/rate-limit 연동은 platform 소유 port/adapter로 추상화한다.
- 예시 경계는 `PlatformTokenIssuerPort`, `PlatformSessionSupport`, `PlatformInternalTokenValidator`, `PlatformAuthenticationDecision`, `PlatformRateLimitDecision`, `PlatformRateLimitPort`처럼 platform prefix를 가진 타입으로 둔다.
- 1계층 `TokenService`, `SessionStore`, `SessionPrincipalMapper`, `RateLimiter`가 필요하면 adapter 계층이 이를 감싸고, auto-configuration과 policy enforcer는 `Platform...Port` 같은 platform 계약만 기준으로 사용한다.
- token/session issuance 공개 계약은 `PlatformIssueTokenCommand`, `PlatformIssueSessionCommand`, `PlatformIssuedToken`, `PlatformSessionView`처럼 orchestration 목적 runtime view로 닫는다.
- `PlatformRateLimitPort`는 service-facing 공개 계약이고, `PlatformRateLimitAdapter`는 backing implementation을 연결하는 adapter marker로만 둔다.
- `OperationalSecurityPolicyEnforcer` 같은 policy는 `PlatformAuthenticationDecision`, `PlatformRateLimitDecision` 같은 platform 소유 decision만 보고 판단한다.
- `PlatformSecurityAutoConfiguration`의 auth wiring은 raw `com.auth.*` bean graph에 직접 결합하지 않고 platform 소유 auth adapter/resolver 계약을 통해 조립한다.
- `@ConditionalOnBean`과 운영 guard는 1계층 bean 존재 여부가 아니라 platform 소유 bean 존재 여부를 기준으로 동작해야 한다.

## Runtime View Model Rule

- `platform-security`는 runtime/orchestration 관점의 view 모델은 가질 수 있다.
- 예: `SecurityRequest`, `SecurityContext`, `PlatformRateLimitRequest`, `PlatformRateLimitDecision`
- 하지만 1계층 `Principal`, `TokenService`, `SessionStore`를 사실상 다시 만든 canonical auth 모델이나 service 계약을 새로 만들면 안 된다.
- `PlatformAuthenticatedPrincipal` 같은 타입이 남아 있다면 이는 공통 runtime view로만 취급하고, 1계층 principal의 영구 대체 canonical model처럼 확장하지 않는다.
- token/session issuance나 lookup 계약은 가능하면 principal 전체 복제보다 issue request, session lookup, issued credential view 같은 runtime 목적 DTO로 닫는 방향을 우선한다.

## platform-security 모듈 기준

현재 platform-security 최신 구조는 아래 모듈 축을 가진다.

- `platform-security-bom`
- `platform-policy-api`
- `platform-security-policy`
- `platform-security-api`
- `platform-security-ports`
- `platform-security-adapter-auth`
- `platform-security-ip`
- `platform-security-adapter-ratelimiter`
- `platform-security-core`
- `platform-security-web`
- `platform-security-autoconfigure`
- `platform-security-issuer-autoconfigure`
- `platform-security-internal-autoconfigure`
- `platform-security-policyconfig-bridge`
- `platform-security-starter`
- `platform-security-support-local`
- `platform-security-client`
- `platform-security-test-support`
- `platform-security-hybrid-web-adapter`
- `platform-security-sample-consumer`

`platform-security-sample-consumer`는 내부 검증용 소비 예제로 본다.

## 포함해야 할 것

- boundary / client type / auth mode / evaluation result 모델
- platform 소유 auth/rate-limit decision / adapter 계약
- authentication / IP guard / rate limit 실행 체인
- Spring Security resource server 기본 조립
- gateway header 기반 인증 조립
- downstream identity propagation
- Spring Boot auto-configuration
- auth wiring 추가 추상화
- 단일 starter와 service role preset
- 운영 fail-fast 정책
- 소비자별 override point
- 실패 응답 표준화
- governance audit 연동을 위한 공개 `SecurityAuditPublisher` 계약
- starter 전면 자동 등록이 어려운 edge/gateway를 위한 공식 hybrid gateway integration surface

## Spring Security 기본 조립 기준

- `platform-security`는 기본 `JwtDecoder`를 제공한다.
- 기본 `JwtDecoder`는 `platform.security.auth.jwt-secret`, `platform.security.auth.jwt-issuer`, `platform.security.auth.jwt-audience` 설정으로 HMAC JWT 검증을 구성한다.
- `platform-security`는 기본 `JwtAuthenticationConverter`를 제공한다.
- 기본 JWT authority 변환은 `role`, `roles`, `scope`, `scp`, `status` claim을 사용한다.
- `status=A`는 `STATUS_A`와 함께 `STATUS_ACTIVE` authority로 표현한다.
- gateway header 인증은 `platform.security.auth.gateway-header.enabled=true`일 때 활성화한다.
- gateway header 인증은 `X-User-Id`, `X-User-Status`를 읽어 Servlet에서는 Spring Security `Authentication`, WebFlux에서는 `GatewayUserPrincipal` 기반 principal을 만든다.
- Servlet gateway header 인증 filter는 `FilterRegistrationBean#setEnabled(false)`로 Boot servlet filter 중복 등록을 막고 Spring Security filter chain 안에서만 동작해야 한다.
- 401/403 응답은 기본 `AuthenticationEntryPoint`, `AccessDeniedHandler`를 통해 `SecurityFailureResponseWriter` 흐름으로 연결한다.
- servlet filter 순서는 `BearerTokenAuthenticationFilter` 뒤에 gateway header 인증 filter를 두고, 그 뒤에 `PlatformSecurityServletFilter`를 둔다.
- gateway header 인증 filter가 없으면 `PlatformSecurityServletFilter`는 `BearerTokenAuthenticationFilter` 뒤에 둔다.
- WebFlux gateway는 `PlatformSecurityReactiveGatewayIntegration`이 제공하는 reactive gateway header `WebFilter` 뒤에 `PlatformSecurityWebFilter`를 두는 구성을 표준으로 본다.
- `PlatformSecurityAutoConfiguration`은 auth wiring을 platform 소유 auth adapter/resolver 계약으로 조립하고 raw `com.auth.*` bean graph를 공개 wiring 기준으로 삼지 않는다.

## 포함하지 말아야 할 것

- 회원가입 비즈니스
- 로그인 화면
- 포인트 정책
- 게시글 권한 규칙
- 문서 수정 권한의 도메인 판단
- 특정 소비자 전용 컨트롤러 비즈니스 로직
- 특정 소비자 URL 하드코딩
- 특정 소비자 Redis key 규칙
- 1계층 OSS 내부 구현 재정의
- 소비자 서비스별 `JwtDecoder` 직접 조립
- 소비자 서비스별 JWT authority converter 직접 조립
- 소비자 서비스별 gateway header authentication filter/principal 직접 조립
- 소비자 서비스가 `com.auth.*`나 1계층 `RateLimiter` 타입을 platform 계약처럼 맞춰 노출해야만 성립하는 구조
- `platform-security-adapter-auth` 공개 API에 `com.auth.*` raw 타입을 영구 계약처럼 고정하는 구조
- `platform-security-ports` 대신 adapter 모듈이 public contract 역할을 떠안는 구조
- `PlatformRateLimitPort`, policy, gateway adapter가 raw `RateLimiter`나 1계층 decision/spi를 그대로 노출하는 구조
- `PlatformSecurityAutoConfiguration`이 raw `com.auth.*` bean graph에 직접 결합된 구조

## 확장 규칙

- public surface는 설정과 확장 bean으로만 넓힌다.
- 모듈 추가는 responsibility first로 한다.
- 1계층 내부 구현을 2계층에서 재정의하지 않는다.
- starter 추가는 역할이 분명할 때만 허용한다.
- governance audit bridge는 `platform-security` 본체가 아니라 `platform-integrations`에서 제공한다.
- `platform-security` 본체는 `platform-governance` 구현체를 직접 의존하지 않는다.
- 소비자 서비스가 직접 인증 조립을 override할 때도 public bean override 경계를 사용하고 platform filter 순서를 깨지 않는다.
- gateway/edge 서비스처럼 starter 기본 filter auto-registration을 그대로 쓸 수 없는 경우를 위해 공식 hybrid adapter module을 둘 수 있다.
- hybrid adapter는 `SecurityPolicyService`, `SecurityIngressAdapter`, auth adapter, rate-limit decision adapter, failure writer, audit publisher처럼 gateway가 직접 소비할 안전한 조립 포인트만 노출해야 한다.
- gateway 통합은 hybrid adapter를 공식 표면으로 사용하고 `platform-security-core`나 `platform-security-web` 내부 wiring을 직접 재조립하지 않는다.
- hybrid adapter는 Servlet용 `PlatformSecurityGatewayIntegration`과 WebFlux용 `PlatformSecurityReactiveGatewayIntegration`을 공식 표면으로 제공할 수 있다.
- strict 목표는 gateway가 `SecurityIngressAdapter` 같은 내부 bean graph 대신 `HybridSecurityRuntime`, `HybridFailureResponseContract`, `HybridHeaderAuthenticationAdapter` 같은 platform-owned runtime surface만 보도록 수렴하는 것이다.
- gateway가 `platform-security-core`나 `platform-security-web` 내부 구현을 직접 조립하는 방식은 표준 경계로 보지 않는다.

## 운영 프로필과 fail-fast 기준

- production profile 기본값은 `["prod", "production"]`를 사용한다.
- 운영 fail-fast는 공통 일괄 강제가 아니라 `service-role-preset`별 규칙으로 설계한다.
- `EDGE`, `API_SERVER`는 IP guard, 분산 rate-limit, trusted proxy 같은 ingress 통제를 강하게 요구할 수 있다.
- `INTERNAL_SERVICE`는 ingress 노출 수준이 다르므로 완화 가능한 예외 스위치를 둘 수 있다.
- `ISSUER`는 token/session 발급 책임에 맞는 별도 fail-fast를 가진다.
- 운영 예외는 `allow-ip-guard-disabled-in-production`, `allow-rate-limit-disabled-in-production`, `allow-non-distributed-rate-limiter-in-production`처럼 명시적 opt-out으로만 허용한다.

## 운영 기준

- 2계층은 내부 소비자 호환성을 우선한다.
- 2계층은 external OSS처럼 외부 semver 호환성을 약속하지 않는다.
- 운영에서는 trusted proxy CIDR, admin/internal IP rule, platform 소유 분산 rate-limit adapter, production `SecurityContextResolver`를 fail-fast 대상으로 보되 preset별 요구 수준을 구분한다.
- 기본 in-memory rate-limit adapter와 dev fallback resolver는 local/test용으로 본다.
- 소비자 서비스의 DB 상태 확인, 업무 권한 판단, endpoint별 도메인 정책은 `platform-security`가 아니라 소비자 서비스 책임이다.
- 변경은 문서, build, workflow를 한 단위로 맞춘다.
- 레포별 공개 문서는 이 표준의 경계를 반복 구현하지 않고 필요한 소비 기준만 적는다.
