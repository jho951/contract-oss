# platform-security

`platform-security`는 `auth`, `ip-guard`, `rate-limiter`를 흡수하는 2계층 security platform이다.

## 책임

- 인증
- 접근 제어
- 요청 진입 보안
- 요청량 제한
- security integration API 제공

## 권장 모듈

- `platform-security-api`
- `platform-security-core`
- `platform-security-spring`
- `platform-security-autoconfigure`
- `platform-security-spring-boot-starter`
- `platform-security-common-test`

## 모듈 설명

- `platform-security-api`: 외부 노출용 security integration API
- `platform-security-core`: auth / ip-guard / rate-limiter 조립 핵심
- `platform-security-spring`: Spring 어댑터
- `platform-security-autoconfigure`: 자동 설정
- `platform-security-spring-boot-starter`: 소비 진입점
- `platform-security-common-test`: 공용 테스트 지원

## 제외 범위

- 정책 저장
- 감사 저장
- 파일 저장
- 서비스 비즈니스 로직

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)
