# CONTRACT_SYNC - ip-guard

이 문서는 `ip-guard` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `ip-guard`
- 대상 역할: IP 허용/차단, 요청 진입 보안 제어

## `ip-guard` 레포가 가져가야 하는 것

- IP allowlist / denylist 판단
- 요청 진입 차단/허용 규칙
- core 엔진
- Spring Boot 연동

## `ip-guard` 레포가 가져가면 안 되는 것

- 인증 토큰 발급
- principal 생성
- 정책 저장소 책임
- 감사 로그 저장 책임
- 파일 저장 책임

## `oss-contract`에서 참조해야 하는 문서

- `registry/current-oss.md`
- `registry/observed-roles.md`
- `registry/mapping.md`
- `registry/dependency-rules.md`
- `registry/repo-roles.md`
- `CONTRACT_SYNC.md`

## 동기화 절차

1. `ip-guard`의 역할을 IP 제어로 고정한다.
2. core와 Spring 연동을 분리해서 문서화한다.
3. 인증, 정책, 저장 책임과 겹치지 않게 정리한다.
4. public 계약과 내부 구현을 분리한다.

## 문구 기준

- `ip-guard`는 요청 진입 보안 라이브러리다.
- `ip-guard`는 IP 기반 허용/차단을 담당한다.
- `ip-guard`는 인증 자체를 책임지지 않는다.

## 체크리스트

- [ ] IP 허용/차단 책임이 분명한가
- [ ] core와 Spring 연동이 분리되어 있는가
- [ ] auth/policy/storage 책임과 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

