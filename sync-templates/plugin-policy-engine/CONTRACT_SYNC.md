# CONTRACT_SYNC - plugin-policy-engine

이 문서는 `plugin-policy-engine` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `plugin-policy-engine`
- 대상 역할: rollout / targeting / variant 평가용 정책 엔진

## `plugin-policy-engine` 레포가 가져가야 하는 것

- 정책 조합
- 정책 평가
- rollout 판단
- targeting 판단
- variant 선택
- Spring Boot 연동

## `plugin-policy-engine` 레포가 가져가면 안 되는 것

- 정책 키/설정 소스 조회 자체
- 감사 로그 저장
- 인증 토큰 발급
- 파일 저장 구현
- 서비스 전용 비즈니스 규칙

## `oss-contract`에서 참조해야 하는 문서

- `registry/current-oss.md`
- `registry/observed-roles.md`
- `registry/mapping.md`
- `registry/dependency-rules.md`
- `registry/repo-roles.md`
- `CONTRACT_SYNC.md`

## 동기화 절차

1. rollout/targeting/variant 평가 책임을 고정한다.
2. policy-config와 역할을 분리한다.
3. audit/security/storage 책임을 침범하지 않도록 한다.
4. public 계약과 내부 구현을 분리한다.

## 문구 기준

- `plugin-policy-engine`은 정책 조합과 평가를 담당한다.
- `plugin-policy-engine`은 정책 값 조회 저장소가 아니다.
- `plugin-policy-engine`은 감사 저장을 책임지지 않는다.

## 체크리스트

- [ ] rollout/targeting/variant 평가가 명확한가
- [ ] policy-config와 경계가 분리되는가
- [ ] auth/audit/storage 책임과 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

