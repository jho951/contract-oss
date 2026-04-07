# platform-security ip-guard

`ip-guard`는 `platform-security`의 IP 접근 제어 구현 레포다.

## 책임

- IP 허용/차단
- 요청 진입 제어
- core 판단 로직
- Spring 연동

## 권장 모듈

- IP allowlist / denylist
- 요청 진입 보안
- core 엔진
- Spring adapter

## 모듈 설명

- `ip-guard-core`: IP 판단 규칙
- `ip-guard-spring`: Spring 어댑터
- `ip-guard-spring-boot-starter`: 소비 진입점

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
5. [docs/access-flow.md](docs/access-flow.md)
