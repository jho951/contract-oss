# CONTRACT_SYNC - auth

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `auth`

## 확인된 역할

- 인증 처리 라이브러리
- principal / token / session 중심
- JWT / OAuth2 / Spring 연동 분리

## SCM 메타데이터 기준

- `github_org`: `jho951`
- `github_repo`: `auth`
- `url`, `connection`, `developerConnection`은 위 두 키를 조립해서 만든다.
- SCM URL을 build.gradle에 하드코딩하지 않는다.

## 반영 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/extension-guide.md`
- `docs/oauth2-design.md`
- `build.gradle`
- `settings.gradle`
- `.github/workflows/publish.yml`
