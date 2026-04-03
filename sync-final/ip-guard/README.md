# platform-security ip-guard

`ip-guard`는 `platform-security`의 IP 접근 제어 구현 레포다.

## 책임

- IP 허용/차단
- 요청 진입 제어
- core 판단 로직
- Spring 연동

## 기준

- 공통 계약과 경계 규칙은 [oss-contract](https://github.com/jho951/oss-contract)를 따른다.
- 실제 서비스 서버의 계약은 [service-contract](https://github.com/jho951/service-contract)를 따른다.

## 범위

- IP allowlist / denylist
- 요청 진입 보안
- core 엔진
- Spring adapter

## 제외 범위

- 인증 token 발급
- principal 생성
- 정책 저장
- 감사 저장
- 파일 저장

## 문서

1. [docs/README.md](docs/README.md)
2. [docs/architecture.md](docs/architecture.md)
3. [docs/modules.md](docs/modules.md)
4. [docs/extension-guide.md](docs/extension-guide.md)

