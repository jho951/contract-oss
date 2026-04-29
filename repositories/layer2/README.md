# 2계층 Platform

이 문서는 현재 `main` 기준으로 조직 표준 4개 플랫폼 레포가 어떤 public surface와 실행 표준으로 정리됐는지 보여준다.
여기 적힌 4개는 현재 운영 중인 공식 line 카탈로그이지, 가능한 2계층 platform 구현 전체 목록은 아니다.

## 한눈에 보기

| 레포 | 현재 역할 | 서비스가 보는 대표 surface | 주로 감싸는 OSS | 설명 |
| --- | --- | --- | --- | --- |
| `platform-security` | 인증과 인가 실행 플랫폼 | `platform-security-starter`, `platform-security-client` | `auth`, `ip-guard`, `rate-limiter` | [설명](platform-security/README.md) |
| `platform-governance` | 감사와 정책과 운영 통제 플랫폼 | governance starter, `ViolationHandler` 포함 public SPI | `audit-log`, `policy-config`, `plugin-policy-engine` | [설명](platform-governance/README.md) |
| `platform-resource` | 파일과 리소스 lifecycle 플랫폼 | `platform-resource-starter`, filestorage/notification bridge starter | `file-storage`, `notification` | [설명](platform-resource/README.md) |
| `platform-integrations` | 알림과 외부 연동 outbound 플랫폼 | `platform-integrations-starter`, `PlatformOutboundSender` | `notification` | [설명](platform-integrations/README.md) |

## 현재 반영된 L5 포인트

- 현재 security 공식 line인 `platform-security`는 `platform-security-client`와 sanctioned bridge starter를 포함한 보안 실행 표준으로 정리됐다.
- `platform-governance`는 `ViolationHandler`까지 포함한 public SPI를 고정했고, `-PuseLocalLayer1=true` 검증 경로도 유지한다.
- `platform-resource`는 raw storage/notification bean을 서비스가 직접 묶지 않도록 bridge starter 두 개를 공식 surface로 올렸다.
- `platform-integrations`는 bridge 중심 설명에서 벗어나, `PlatformOutboundSender`를 중심으로 한 outbound platform으로 정리됐다.
- 네 레포 모두 published surface, starter contract, sample consumer, Stage5 contract gate를 기본 품질 기준으로 둔다.

## 소비 기준

- 서비스는 OSS를 직접 보지 않고 platform starter, platform port, platform-owned SPI만 소비한다.
- 다른 2계층 platform line도 같은 1계층 OSS를 감싸서 나올 수 있다.
- published surface는 각 line의 배포 단위이지, 특정 platform 이름으로 영구 고정하자는 뜻이 아니다.
- 1계층 타입을 platform public surface로 다시 내보내면 L5 완료로 보지 않는다.
- 현재 구현 이력과 과거 version 정리는 [../../troubleshooting.md](../../troubleshooting.md)에 남긴다.
- 목표 구조와 전환 순서는 `registry/layer2` 기준 문서를 source-of-truth로 본다.
