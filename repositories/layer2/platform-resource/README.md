# platform-resource

## 기준

- GitHub: https://github.com/jho951/platform-resource
- Version: `1.0.0`
- 계층: 2계층 platform
- registry 기준: [../../../registry/layer2/README.md](../../../registry/layer2/README.md)

## 흡수 대상

- `file-storage`
- `notification`

## 책임

- 리소스 소유자
- kind
- metadata catalog
- 접근 판단
- 저장 / 삭제 생명주기 알림 orchestration
- file-storage / notification primitive 조립

## 현재 모듈

- `platform-resource-bom`
- `platform-resource-api`
- `platform-resource-spi`
- `platform-resource-core`
- `platform-resource-filestorage-adapter`
- `platform-resource-notification-adapter`
- `platform-resource-jdbc`
- `platform-resource-local`
- `platform-resource-autoconfigure`
- `platform-resource-starter`

## 현재 문서

- `README.md`
- `docs/README.md`
- `docs/architecture.md`
- `docs/modules.md`
- `docs/usage.md`

## 정리 후보

- `CONTRACT_SYNC.md` 제거
- `.github/workflows/build.yml` 추가 여부 확인
- `docs/extension-guide.md` 필요 여부 확인
- `platform-resource` 사용 기준 문서를 구현 레포에 반영할지 확인
