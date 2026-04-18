# platform-security Standard

이 문서는 `platform-security` 2계층 platform의 표준 구조와 경계를 고정한다.

## 목적

- `auth`, `ip-guard`, `rate-limiter` 1계층 OSS를 조립하는 표준 2계층을 정의한다.
- 공통 보안 파이프라인을 표준화한다.
- platform 소비자가 쉽게 가져다 쓸 수 있는 내부 비공개 platform 경계를 고정한다.

## 계층 원칙

- 1계층 OSS는 공개 배포 가능한 독립 라이브러리로 취급한다.
- 2계층 `platform-security`는 1계층 OSS를 조합하는 내부 비공개 platform layer로 취급한다.
- 2계층은 범용 설계를 유지하되 외부 공개 라이브러리처럼 소비되는 계층이 아니다.
- 2계층의 공개 표면은 내부 소비자 공통 사용을 전제로 한다.
- 확장은 `properties`, `customizer`, `override bean`, 단일 starter, service role preset을 통해 제공한다.
- 현재 소비 진입점은 단일 `platform-security-starter`와 `platform.security.service-role-preset`이다.
- 2계층은 소비자별 비즈니스 로직, 도메인 권한 판단, 회원가입, 로그인 화면, 특정 URL, Redis key 규칙을 포함하지 않는다.

## 1계층 조립 기준

- `auth`: `auth-core`, `auth-jwt`, `auth-session`, `auth-hybrid`, `auth-apikey`, `auth-hmac`, `auth-oidc`, `auth-service-account`
- `ip-guard`: `ip-guard-core`, `ip-guard-spi`
- `rate-limiter`: `rate-limiter-core`, `rate-limiter-spi`

## platform-security 모듈 기준

현재 platform-security 최신 구조는 아래 모듈 축을 가진다.

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

`platform-security-sample-consumer`는 내부 검증용 소비 예제로 본다.

## 포함해야 할 것

- boundary / client type / auth mode / evaluation result 모델
- authentication / IP guard / rate limit 실행 체인
- downstream identity propagation
- Spring Boot auto-configuration
- 단일 starter와 service role preset
- 운영 fail-fast 정책
- 소비자별 override point
- 실패 응답 표준화
- governance audit 연동을 위한 공개 `SecurityAuditPublisher` 계약

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

## 확장 규칙

- public surface는 설정과 확장 bean으로만 넓힌다.
- 모듈 추가는 responsibility first로 한다.
- 1계층 내부 구현을 2계층에서 재정의하지 않는다.
- starter 추가는 역할이 분명할 때만 허용한다.
- governance audit bridge는 `platform-security` 본체가 아니라 `platform-integrations`에서 제공한다.

## 운영 기준

- 2계층은 내부 소비자 호환성을 우선한다.
- 2계층은 external OSS처럼 외부 semver 호환성을 약속하지 않는다.
- 운영에서는 trusted proxy CIDR, admin/internal IP rule, 공유 `RateLimiter`, production `SecurityContextResolver`를 fail-fast로 요구한다.
- 기본 in-memory rate limiter와 dev fallback resolver는 local/test용으로 본다.
- 변경은 문서, build, workflow를 한 단위로 맞춘다.
- 레포별 공개 문서는 이 표준의 경계를 반복 구현하지 않고 필요한 소비 기준만 적는다.
