# CONTRACT_SYNC - notification

이 문서는 `notification` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `notification`
- 대상 상태: 작성 전

## 현재 원칙

- 현재는 빈 레포이므로 역할을 미리 과하게 정의하지 않는다.
- 기능이 생기면 그 기능이 `platform-governance`, `platform-security`, `platform-storage` 중 어디에 속하는지 다시 판단한다.
- 역할이 정해지기 전까지는 분류 보류 상태로 둔다.

## 동기화 절차

1. 기능이 추가되기 전까지는 `notification`의 책임을 확정하지 않는다.
2. 실제 구현이 생기면 읽기/쓰기 책임을 확인한다.
3. 그 책임이 플랫폼 계층에 들어가는지, 별도 OSS로 유지할지 판단한다.
4. `oss-contract`의 매핑 문서에 반영한다.

## 문구 기준

- `notification`은 현재 작성 전 레포다.
- `notification`은 아직 platform 흡수 대상을 고정하지 않는다.

## 체크리스트

- [ ] 현재 비어 있는 상태를 명시했는가
- [ ] 역할을 과도하게 추정하지 않았는가
- [ ] 추후 분류 보류 상태가 드러나는가

