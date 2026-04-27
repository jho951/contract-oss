# 2계층 Platform

이 문서는 main 브랜치 기준 L5 목표 구조에서 4개 플랫폼이 어떤 역할로 정리되는지 보여준다.

| 레포 | 목표 역할 | 표준 | 주로 감싸는 OSS | 상태 |
| --- | --- | --- | --- | --- |
| `platform-security` | 인증과 인가 실행 플랫폼 | [표준](../../registry/layer2/standards/platform-security.md) | `auth`, `ip-guard`, `rate-limiter` | [설명](platform-security/README.md) |
| `platform-governance` | 감사와 정책과 운영 통제 플랫폼 | [표준](../../registry/layer2/standards/platform-governance.md) | `audit-log`, `policy-config`, `plugin-policy-engine` | [설명](platform-governance/README.md) |
| `platform-resource` | 파일과 리소스 lifecycle 플랫폼 | [표준](../../registry/layer2/standards/platform-resource.md) | `file-storage`, `notification` | [설명](platform-resource/README.md) |
| `platform-integrations` | 알림과 외부 연동 outbound 플랫폼 | [표준](../../registry/layer2/standards/platform-integrations.md) | `notification` | [설명](platform-integrations/README.md) |

## 소비 기준

- 서비스는 OSS를 직접 보지 않고 platform만 소비한다.
- `platform-security`, `platform-governance`, `platform-resource`, `platform-integrations`는 모두 서비스 코드에서 공통 실행 흐름을 걷어내기 위한 계층이다.
- 현재 구현 이력과 과거 version 정리는 [../../troubleshooting.md](../../troubleshooting.md)에 남긴다.
- 목표 구조와 전환 순서는 `registry/layer2` 기준 문서를 source-of-truth로 본다.
