# oss-contract

- 현재 존재하는 1계층 OSS 레포들과, 앞으로 만들 2계층 platform 구조의 관계를 한 곳에서 관리한다.
- 앞으로 만들어질 3계층 service 구조와의 관계까지 함께 관리한다.
- 공통 계약과 경계 규칙을 하나의 SOT로 둔다.
- 어떤 OSS가 어떤 platform으로 흡수되는지 기준을 고정한다.
- 2계층 platform은 실제 서비스 서버들이 `service-contract` 기준으로 소비하는 기반 계층이다.

## 시작점

1. [registry/README.md](registry/README.md)
2. [registry/layers.md](registry/layers.md)
3. [registry/mapping.md](registry/mapping.md)
4. [registry/dependency-rules.md](registry/dependency-rules.md)
5. [registry/repo-roles.md](registry/repo-roles.md)
6. [registry/current-oss.md](registry/current-oss.md)
7. [registry/future-platforms.md](registry/future-platforms.md)
8. [registry/service-layer.md](registry/service-layer.md)
9. [registry/service-contract.md](registry/service-contract.md)
10. [registry/sync-order.md](registry/sync-order.md)
11. [registry/access-procedure.md](registry/access-procedure.md)
12. [registry/github-local-approach.md](registry/github-local-approach.md)
13. [registry/layer1-structure.md](registry/layer1-structure.md)
14. [registry/layer1-module-policy.md](registry/layer1-module-policy.md)
15. [registry/layer1-build-standard.md](registry/layer1-build-standard.md)
16. [registry/layer1-workflow-standard.md](registry/layer1-workflow-standard.md)
17. [registry/versioning-standard.md](registry/versioning-standard.md)
18. [registry/notification-policy.md](registry/notification-policy.md)
19. [registry/final-apply-order.md](registry/final-apply-order.md)
20. [registry/operation-rules.md](registry/operation-rules.md)
21. [registry/apply-guide.md](registry/apply-guide.md)
22. [registry/release-execution-order.md](registry/release-execution-order.md)
22. [repositories/README.md](repositories/README.md)
23. [repositories/auth.md](repositories/auth.md)
24. [repositories/ip-guard.md](repositories/ip-guard.md)
25. [repositories/rate-limiter.md](repositories/rate-limiter.md)
26. [repositories/audit-log.md](repositories/audit-log.md)
27. [repositories/policy-config.md](repositories/policy-config.md)
28. [repositories/plugin-policy-engine.md](repositories/plugin-policy-engine.md)
29. [repositories/file-storage-module.md](repositories/file-storage-module.md)
30. [repositories/notification.md](repositories/notification.md)
31. [repositories/platform-security.md](repositories/platform-security.md)
32. [repositories/platform-governance.md](repositories/platform-governance.md)
33. [repositories/platform-storage.md](repositories/platform-storage.md)
34. [repositories/service-contract.md](repositories/service-contract.md)
35. [CONTRACT_SYNC.md](CONTRACT_SYNC.md)
36. [sync-templates/auth/CONTRACT_SYNC.md](sync-templates/auth/CONTRACT_SYNC.md)

## 원칙

- 구현은 이 레포에 두지 않는다.
- 계약과 경계 규칙만 이 레포에서 관리한다.
- private 플랫폼의 내부 문서는 별도 레포에서 관리한다.
