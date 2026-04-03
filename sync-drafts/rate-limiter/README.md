# platform-security rate-limiter

이 저장소는 `platform-security`의 요청 속도 제한 구현 레포다.

## 역할

- IP 기준 rate limit
- 사용자 ID 기준 rate limit
- API 키 기준 rate limit
- in-memory 제한
- Redis 기반 분산 제한
- Spring Boot 연동

## 기준 문서

- 공통 계약과 경계 규칙은 [oss-contract](https://github.com/jho951/oss-contract)를 기준으로 한다.
- 실제 서비스 서버의 계약은 [service-contract](https://github.com/jho951/service-contract)를 기준으로 한다.

## 포함 범위

- IP / 사용자 ID / API 키 기준 제한
- in-memory token bucket
- Redis 기반 분산 제한
- Spring Boot adapter

## 제외 범위

- 인증 principal 생성
- 정책 엔진 평가
- 감사 로그 저장
- 파일 저장

## 문서 진입점

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)

