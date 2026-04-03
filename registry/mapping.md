# OSS 매핑

`notification`은 현재 작성 전 상태라서, 아직 2계층 흡수 대상으로 고정하지 않는다.

| 1계층 OSS | 2계층 플랫폼 | 책임 |
| --- | --- | --- |
| `auth` | `platform-security` | 인증 처리, principal/token/session |
| `ip-guard` | `platform-security` | IP 허용/차단 |
| `rate-limiter` | `platform-security` | 요청 속도 제어 |
| `audit-log` | `platform-governance` | 구조화 감사 로그 |
| `policy-config` | `platform-governance` | 정책 키/설정 소스 조회 |
| `plugin-policy-engine` | `platform-governance` | 정책 조합/평가 |
| `file-storage-module` | `file-storage` | 파일 저장 추상화 |

## 해석 규칙

- `notification`은 별도 OSS로 유지하거나, 향후 platform 소비 구조가 정해지면 재분류한다.
- `auth`, `ip-guard`, `rate-limiter`는 요청 진입 보안 영역이다.
- `audit-log`, `policy-config`, `plugin-policy-engine`는 거버넌스 영역이다.
- `file-storage-module`은 스토리지 영역이며 실제 GitHub 레포명은 `file-storage`다.
