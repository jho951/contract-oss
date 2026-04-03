# CONTRACT_SYNC - policy-config

이 문서는 `policy-config` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `policy-config`
- 대상 역할: 정책 키와 설정 소스 조회

## `policy-config` 레포가 가져가야 하는 것

- 환경변수 조회
- System Properties 조회
- `.properties` 조회
- `Map` 기반 조회
- 타입 안전한 `PolicyKey<T>` 조회
- Spring Boot 자동 설정

## `policy-config` 레포가 가져가면 안 되는 것

- 정책 실행 엔진
- 감사 로그 저장
- 인증 토큰 처리
- 파일 저장
- 서비스 비즈니스 규칙

## `oss-contract`에서 참조해야 하는 문서

- `registry/current-oss.md`
- `registry/observed-roles.md`
- `registry/mapping.md`
- `registry/dependency-rules.md`
- `registry/repo-roles.md`
- `CONTRACT_SYNC.md`

## 동기화 절차

1. 정책 키 조회 책임을 고정한다.
2. 설정 소스 해석 책임만 남긴다.
3. 정책 실행과 정책 저장을 분리한다.
4. public 계약과 내부 구현을 분리한다.

## 문구 기준

- `policy-config`는 설정/정책 키 조회 라이브러리다.
- `policy-config`는 정책 값을 읽는 기준이다.
- `policy-config`는 정책을 실행하지 않는다.

## 체크리스트

- [ ] 설정 소스 조회 책임이 명확한가
- [ ] 타입 안전한 키 조회가 드러나는가
- [ ] engine/audit/storage 책임과 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

