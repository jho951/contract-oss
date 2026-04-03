# CONTRACT_SYNC - rate-limiter

이 문서는 `rate-limiter` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `rate-limiter`
- 대상 역할: 요청 속도 제한

## `rate-limiter` 레포가 가져가야 하는 것

- IP 기준 rate limit
- 사용자 ID 기준 rate limit
- API 키 기준 rate limit
- in-memory 제한
- Redis 기반 분산 제한
- Spring Boot 연동

## `rate-limiter` 레포가 가져가면 안 되는 것

- 인증 principal 생성
- 정책 엔진 평가
- 감사 로그 저장
- 파일 저장
- 서비스 고유 비즈니스 규칙

## `oss-contract`에서 참조해야 하는 문서

- `registry/current-oss.md`
- `registry/observed-roles.md`
- `registry/mapping.md`
- `registry/dependency-rules.md`
- `registry/repo-roles.md`
- `CONTRACT_SYNC.md`

## 동기화 절차

1. rate limit 기준을 IP / 사용자 / API 키로 고정한다.
2. in-memory와 Redis 구현을 분리해서 문서화한다.
3. 인증과 정책 평가 책임을 넘지 않도록 한다.
4. public 계약과 내부 구현을 분리한다.

## 문구 기준

- `rate-limiter`는 요청 속도 제한 라이브러리다.
- `rate-limiter`는 서비스 진입점의 과도한 호출을 제어한다.
- `rate-limiter`는 인증과 정책 결정을 책임지지 않는다.

## 체크리스트

- [ ] rate limit 기준이 명확한가
- [ ] in-memory와 Redis가 구분되어 있는가
- [ ] auth/policy/storage 책임과 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

