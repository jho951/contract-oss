# 2계층 Platform

| 레포 | Version | 성격 | 표준 | 흡수 대상 | GitHub | 상태 |
| --- | --- | --- | --- | --- | --- | --- |
| `platform-security` | `2.0.3` | runtime platform | [표준](../../registry/layer2/standards/platform-security.md) | `auth`, `ip-guard`, `rate-limiter` | https://github.com/jho951/platform-security | [상태](platform-security/README.md) |
| `platform-governance` | `2.0.1` | runtime platform | [표준](../../registry/layer2/standards/platform-governance.md) | `audit-log`, `policy-config`, `plugin-policy-engine-config` 호환 | https://github.com/jho951/platform-governance | [상태](platform-governance/README.md) |
| `platform-resource` | `2.0.0` | runtime platform | [표준](../../registry/layer2/standards/platform-resource.md) | `file-storage`, `notification` | https://github.com/jho951/platform-resource | [상태](platform-resource/README.md) |
| `platform-integrations` | `1.0.1` | optional bridge layer | [표준](../../registry/layer2/standards/platform-integrations.md) | platform 간 optional bridge | https://github.com/jho951/platform-integrations | [상태](platform-integrations/README.md) |

## 소비 기준

- `platform-security`, `platform-governance`, `platform-resource`는 서비스가 직접 소비하는 실행 platform이다.
- `platform-integrations`는 두 platform을 모두 쓰는 소비자가 연결 요구가 있을 때만 추가하는 bridge layer다.
- `platform-resource`는 단순 file-storage wrapper가 아니라 resource lifecycle runtime이다.
