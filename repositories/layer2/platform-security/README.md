# platform-security

## 기준

- GitHub: https://github.com/jho951/platform-security
- Version: `2.0.5`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)
- platform 표준: [../../../registry/layer2/standards/platform-security.md](../../../registry/layer2/standards/platform-security.md)

## 흡수 대상

- `auth`
- `ip-guard`
- `rate-limiter`

## 책임

- boundary / client type / auth mode / evaluation result 모델
- platform 소유 auth/rate-limit decision / adapter 계약
- authentication / IP guard / rate limit / downstream identity propagation 실행 체인
- Spring Security 기본 `JwtDecoder`와 `JwtAuthenticationConverter` 조립
- gateway header 기반 인증 컨텍스트 조립
- `PlatformSecurityAutoConfiguration`의 auth wiring 추상화
- 401/403 실패 응답 writer 연결과 servlet filter 순서 조립
- Spring Boot 자동 구성
- 단일 starter와 `service-role-preset`
- 내부 소비자 공통 보안 진입점
- governance audit bridge가 소비할 수 있는 security audit event/publisher 계약
- 보안 평가와 보안 event 발행 경계
- gateway/edge 서비스용 공식 hybrid 통합 표면

## 현재 모듈

- `platform-security-bom`
- `platform-policy-api`
- `platform-security-policy`
- `platform-security-api`
- `platform-security-auth`
- `platform-security-ip`
- `platform-security-rate-limit`
- `platform-security-core`
- `platform-security-web`
- `platform-security-autoconfigure`
- `platform-security-issuer-autoconfigure`
- `platform-security-internal-autoconfigure`
- `platform-security-policyconfig-bridge`
- `platform-security-starter`
- `platform-security-local-support`
- `platform-security-client`
- `platform-security-test-support`
- `platform-security-hybrid-web-adapter`
- `platform-security-sample-consumer`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/quickstart.md`
- `docs/architecture.md`
- `docs/configuration.md`
- `docs/extension-guide.md`
- `docs/modules.md`
- `docs/private-publish.md`
- `docs/release-notes.md`
- `docs/security-model.md`
- `docs/troubleshooting.md`
- `docs/why-use-platform-security.md`

## README / 문서 기준

- 공개 좌표는 실제 publish artifact와 일치해야 한다.
- 흡수 대상은 1계층 기준 버전과 충돌하지 않아야 한다.
- `무엇을 제공하나`는 `settings.gradle` include 목록과 일치해야 한다.
- 책임 경계에는 platform 조립 책임과 소비자 비즈니스 책임을 명확히 나눈다.
- docs는 platform 소비와 확장에 필요한 문서만 둔다.
- `platform-security-auth` 공개 시그니처가 `com.auth.*`를 임시로 노출하면 그 의존성 범위와 제거 계획을 문서에 같이 적는다.
- auth/rate-limit public surface는 raw SPI가 아니라 platform 소유 decision/adapter 계약 기준으로 설명한다.
- 소비자별 비즈니스 정책이나 도메인 권한 판단을 platform 책임처럼 설명하지 않는다.

## 현재 version pin

- `auth_version=3.0.1`
- `ipGuard_version=3.0.0`
- `rateLimiter_version=2.0.0`
- `release_version=2.0.5`

## 실무 기준

- 소비자는 `platform-security-starter`와 `platform.security.service-role-preset`을 기본 진입점으로 사용한다.
- `edge`, `issuer`, `api-server`, `internal-service` preset은 artifact 선택이 아니라 설정 선택이다.
- `platform-security-auth` 공개 API는 최종적으로 `com.auth.*` 의존을 제거해야 하며, 제거 전까지는 공개 시그니처에 남아 있는 타입 의존성을 `api` 범위로 승격해 compile surface를 숨기지 않는다.
- 기본 JWT 검증은 `platform.security.auth.jwt-secret`, `jwt-issuer`, `jwt-audience`로 구성한다.
- 기본 JWT authority 변환은 `role`, `roles`, `scope`, `scp`, `status` claim을 사용하며 active status는 `STATUS_ACTIVE` authority로 표현한다.
- gateway header 인증은 `platform.security.auth.gateway-header.enabled=true`일 때 `X-User-Id`, `X-User-Status`를 Spring Security `Authentication`으로 변환한다.
- 소비자 서비스는 `JwtDecoder`, JWT authority converter, gateway header filter/principal을 직접 재조립하지 않는다.
- `PlatformRateLimitAdapter`는 raw `RateLimiter`를 public contract로 노출하지 않고 platform 소유 rate-limit decision만 반환해야 한다.
- `OperationalSecurityPolicyEnforcer`와 관련 policy는 raw auth/rate-limit SPI가 아니라 platform 소유 decision 계약만 보고 판단해야 한다.
- `PlatformSecurityAutoConfiguration`의 auth wiring은 raw `com.auth.*` bean graph 대신 platform 소유 auth adapter/resolver 추상화를 통해 조립해야 한다.
- 운영에서는 platform 소유 token/session/rate-limit port와 trusted proxy CIDR를 preset-aware fail-fast 대상으로 본다.
- `EDGE`/`API_SERVER`, `INTERNAL_SERVICE`, `ISSUER`는 같은 ingress 규칙으로 묶지 않고 preset별로 다르게 판정한다.
- gateway처럼 starter 기본 filter auto-registration을 그대로 쓰기 어려운 서비스는 `platform-security-hybrid-web-adapter`를 공식 gateway 통합 표면으로 사용한다.
- security event를 governance audit으로 남겨야 할 때만 `platform-integrations`의 `platform-security-governance-bridge`를 추가한다.
- `/users/me` active 상태 확인처럼 서비스 DB 사실에 의존하는 도메인 정책은 소비자 서비스가 소유한다.
- `policy-config`, audit pipeline, feature flag config 호환 기준의 owner는 `platform-governance`다.
- `platform-security`는 `platform-governance` 구현체를 직접 의존하지 않는다.

## 반영 상태

- 1계층 OSS 타입 직접 결합은 platform 소유 port/adapter 기준으로 완화했다.
- `OperationalSecurityPolicyEnforcer`는 preset-aware 규칙과 명시적 예외 스위치 기준으로 재구성됐다.
- 공식 gateway hybrid adapter module이 추가됐다.
- production profile 기본값은 `prod`, `production`으로 통일됐다.
- 구현 레포 `main` push와 `v2.0.5` release까지 완료됐다.
- `platform-security-governance-bridge:1.0.3`는 이 버전을 기준으로 검증되고 배포됐다.
