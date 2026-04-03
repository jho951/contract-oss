# CONTRACT_SYNC - auth

이 문서는 `auth` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `auth`
- 대상 역할: 인증 처리, principal/token/session, JWT/OAuth2/Spring 연동

## `auth` 레포가 가져가야 하는 것

- 인증 흐름
- principal 생성과 전달
- token 발급/검증
- session 처리
- JWT 구현
- OAuth2 구현
- Spring 연동

## `auth` 레포가 가져가면 안 되는 것

- platform-governance 책임
- platform-storage 책임
- 감사 로그 저장 방식
- 정책 엔진 평가 로직
- 파일 저장 구현
- 공통 계약의 재정의

## `oss-contract`에서 참조해야 하는 문서

- `registry/current-oss.md`
- `registry/observed-roles.md`
- `registry/mapping.md`
- `registry/dependency-rules.md`
- `registry/repo-roles.md`
- `CONTRACT_SYNC.md`

## auth 레포에서 확인할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/oauth2-design.md`

## 동기화 절차

1. `auth` 레포 README에서 역할 설명을 `oss-contract`와 일치시킨다.
2. principal/token/session 범위를 명시한다.
3. JWT, OAuth2, Spring 연동 책임을 분리해 적는다.
4. `platform-governance`, `platform-storage` 책임을 침범하지 않는지 확인한다.
5. public 계약과 internal 구현 설명을 구분한다.

## 문구 기준

- `auth`는 인증 처리 라이브러리다.
- `auth`는 요청 진입 보안의 일부다.
- `auth`는 실제 서비스가 사용하는 `platform-security`의 핵심 구성요소다.
- `auth`는 정책 평가나 감사 저장을 책임지지 않는다.

## 체크리스트

- [ ] `auth`의 현재 역할이 인증 중심으로 적혀 있는가
- [ ] principal/token/session 책임이 분명한가
- [ ] JWT/OAuth2/Spring 연동이 분리되어 있는가
- [ ] platform 책임과 구현 책임이 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

## 동기화 기록

- 마지막 동기화 일자:
- 반영 요약:
- 남은 작업:

