# 현재 OSS 목록

현재 확인된 1계층 OSS 레포는 아래 7개다.

| 레포 | 상태 | 비고 |
| --- | --- | --- |
| `auth` | 존재 | 인증 처리, principal/token/session |
| `ip-guard` | 존재 | IP 허용/차단 |
| `rate-limiter` | 존재 | 요청 속도 제한 |
| `audit-log` | 존재 | 구조화 감사 로그 |
| `policy-config` | 존재 | 정책 키/설정 소스 조회 |
| `plugin-policy-engine` | 존재 | 정책 조합/평가 엔진 |
| `file-storage-module` | 존재 | 파일 저장 추상화 |
| `notification` | 작성 전 | 아직 코드/레포가 없다 |

## 주의

- `policy-config`는 하나의 OSS 레포다.
- `notification`은 현재 기준으로는 미구현 항목이다.
