# CONTRACT_SYNC - auth

이 문서는 `auth` 레포에 반영할 동기화 기준이다.

## 기준

- 기준 SOT: `oss-contract`
- 서비스 계약 기준: `service-contract`
- 대상 레포: `auth`

## 확인된 역할

- 인증 처리 라이브러리
- principal / token / session 중심
- JWT / OAuth2 / Spring 연동 분리

## 동기화할 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/oauth2-design.md`

## 문구 기준

- `auth`는 `platform-security`의 인증 구현 레포다.
- `auth`는 요청 진입 보안의 인증 책임을 맡는다.
- `auth`는 정책, 감사, 저장 책임을 가지지 않는다.

