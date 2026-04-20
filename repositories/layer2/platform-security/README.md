# platform-security

## 기준

- GitHub: https://github.com/jho951/platform-security
- Version: `2.0.3`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)
- platform 표준: [../../../registry/layer2/platform-security-standard.md](../../../registry/layer2/platform-security-standard.md)

## 흡수 대상

- `auth`
- `ip-guard`
- `rate-limiter`

## 책임

- boundary / client type / auth mode / evaluation result 모델
- authentication / IP guard / rate limit / downstream identity propagation 실행 체인
- Spring Security 기본 `JwtDecoder`와 `JwtAuthenticationConverter` 조립
- gateway header 기반 인증 컨텍스트 조립
- 401/403 실패 응답 writer 연결과 servlet filter 순서 조립
- Spring Boot 자동 구성
- 단일 starter와 `service-role-preset`
- 내부 소비자 공통 보안 진입점
- governance audit bridge가 소비할 수 있는 security audit event/publisher 계약
- 보안 평가와 보안 event 발행 경계

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

## 현재 version pin

- `auth_version=3.0.1`
- `ipGuard_version=3.0.0`
- `rateLimiter_version=2.0.0`
- `release_version=2.0.3`

## 실무 기준

- 소비자는 `platform-security-starter`와 `platform.security.service-role-preset`을 기본 진입점으로 사용한다.
- `edge`, `issuer`, `api-server`, `internal-service` preset은 artifact 선택이 아니라 설정 선택이다.
- 기본 JWT 검증은 `platform.security.auth.jwt-secret`, `jwt-issuer`, `jwt-audience`로 구성한다.
- 기본 JWT authority 변환은 `role`, `roles`, `scope`, `scp`, `status` claim을 사용하며 active status는 `STATUS_ACTIVE` authority로 표현한다.
- gateway header 인증은 `platform.security.auth.gateway-header.enabled=true`일 때 `X-User-Id`, `X-User-Status`를 Spring Security `Authentication`으로 변환한다.
- 소비자 서비스는 `JwtDecoder`, JWT authority converter, gateway header filter/principal을 직접 재조립하지 않는다.
- 운영에서는 `SecurityContextResolver`, 공유 `RateLimiter`, trusted proxy CIDR, issuer용 token/session bean을 fail-fast 대상으로 본다.
- security event를 governance audit으로 남겨야 할 때만 `platform-integrations`의 `platform-security-governance-bridge`를 추가한다.
- `/users/me` active 상태 확인처럼 서비스 DB 사실에 의존하는 도메인 정책은 소비자 서비스가 소유한다.
- `policy-config`, audit pipeline, feature flag config 호환 기준의 owner는 `platform-governance`다.
- `platform-security`는 `platform-governance` 구현체를 직접 의존하지 않는다.
