# 1계층 최종 적용 순서

이 문서는 1계층 OSS 레포에 최종 표준을 적용할 순서를 정리한다.

## 우선순위

1. `auth`
2. `ip-guard`
3. `rate-limiter`
4. `audit-log`
5. `policy-config`
6. `plugin-policy-engine`
7. `file-storage-module`

## 이유

- `auth`가 기준 레포다.
- `ip-guard`, `rate-limiter`는 같은 security 계층이다.
- `audit-log`, `policy-config`, `plugin-policy-engine`는 governance 계층이다.
- `file-storage-module`은 storage 계층이다.

## 적용 단위

각 레포는 아래 순서로 적용한다.

1. `CONTRACT_SYNC.md`
2. `README.md`
3. `settings.gradle`
4. `build.gradle`
5. `.github/workflows/publish.yml`
6. `docs/README.md`
7. `docs/architecture.md`
8. `docs/modules.md`
9. `docs/extension-guide.md`
10. 필요한 추가 문서

## `notification`

- `notification`은 이 순서에 포함하지 않는다.
- 기능이 생긴 뒤 다시 적용 순서에 넣는다.

