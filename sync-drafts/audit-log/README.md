# platform-governance audit-log

이 저장소는 `platform-governance`의 감사 로그 구현 레포다.

## 역할

- 구조화된 감사 로그 기록
- actor / occurredAt / clientIp / action / resource / result 표준화
- 보안 감사와 운영 추적 재사용
- Spring Boot 연동

## 기준 문서

- 공통 계약과 경계 규칙은 [oss-contract](https://github.com/jho951/oss-contract)를 기준으로 한다.
- 실제 서비스 서버의 계약은 [service-contract](https://github.com/jho951/service-contract)를 기준으로 한다.

## 포함 범위

- 표준 감사 이벤트 모델
- 성공/실패 기록 보조 API
- 민감정보 마스킹
- file sink
- HTTP sink
- async sink 래핑

## 제외 범위

- 인증 토큰 발급
- 정책 엔진 평가
- 파일 저장 기능
- 서비스 비즈니스 로직

## 문서 진입점

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)

