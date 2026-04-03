# 동기화 순서

이 문서는 `oss-contract`를 기준으로 실제 레포에 문서를 적용하는 우선순위를 정의한다.

## 원칙

- 경계가 명확한 것부터 먼저 맞춘다.
- platform-security를 먼저 고정한다.
- 그다음 platform-governance, platform-storage를 맞춘다.
- 마지막에 service-contract와 실제 서비스 레포를 맞춘다.

## 권장 순서

| 순서 | 대상 | 이유 |
| --- | --- | --- |
| 1 | `auth` | 인증은 가장 기본 경계이고 플랫폼 시작점이기 때문이다 |
| 2 | `ip-guard` | 요청 진입 제어로 auth와 같은 보안 계층에 속하기 때문이다 |
| 3 | `rate-limiter` | 보안 진입 제어의 마지막 축이기 때문이다 |
| 4 | `audit-log` | 공통 감사 기준을 먼저 고정해야 뒤의 정책/서비스가 흔들리지 않기 때문이다 |
| 5 | `policy-config` | 정책 키와 설정 조회 기준을 고정해야 정책 엔진과 서비스가 정렬되기 때문이다 |
| 6 | `plugin-policy-engine` | 정책 평가는 설정 조회 기준이 고정된 다음에 맞추는 것이 안전하기 때문이다 |
| 7 | `file-storage-module` | 저장 추상화는 마지막에 맞춰도 다른 계층을 덜 흔들기 때문이다 |
| 8 | `service-contract` | 실제 서비스 계약은 플랫폼 계약이 정리된 뒤에 맞추는 것이 효율적이기 때문이다 |
| 9 | 실제 서비스 레포들 | 최종적으로 서비스들이 platform을 조립하는 문구를 맞춘다 |

## 동기화 단위

각 레포에 대해 아래 순서로 적용한다.

1. `CONTRACT_SYNC.md`
2. `README.md`
3. `docs/README.md`
4. `docs/architecture.md`
5. `docs/modules.md`
6. `docs/extension-guide.md`
7. 필요한 추가 문서

## 지금 기준 추천

- 1차: `auth`
- 2차: `ip-guard`
- 3차: `rate-limiter`
- 4차: `audit-log`
- 5차: `policy-config`
- 6차: `plugin-policy-engine`
- 7차: `file-storage-module`
- 8차: `service-contract`
