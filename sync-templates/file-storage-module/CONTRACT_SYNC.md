# CONTRACT_SYNC - file-storage-module

이 문서는 `file-storage-module` 레포를 `oss-contract` 기준에 맞춰 동기화하기 위한 템플릿이다.

## 기준

- 기준 SOT: `oss-contract`
- 대상 레포: `file-storage-module`
- 대상 역할: 파일 저장 기능 추상화

## `file-storage-module` 레포가 가져가야 하는 것

- 파일 저장 인터페이스
- 저장/조회 추상화
- 파일 경로와 저장 방식의 인터페이스 정의
- 구현체 교체가 가능한 구조

## `file-storage-module` 레포가 가져가면 안 되는 것

- 인증 책임
- 정책 엔진 책임
- 감사 로그 책임
- 서비스 비즈니스 규칙
- 특정 스토리지 벤더 종속 구현을 계약보다 앞세우는 것

## `oss-contract`에서 참조해야 하는 문서

- `registry/current-oss.md`
- `registry/observed-roles.md`
- `registry/mapping.md`
- `registry/dependency-rules.md`
- `registry/repo-roles.md`
- `CONTRACT_SYNC.md`

## 동기화 절차

1. 파일 저장 추상화 책임만 남긴다.
2. 저장/조회 인터페이스를 고정한다.
3. storage 외 책임과 섞이지 않도록 한다.
4. public 계약과 내부 구현을 분리한다.

## 문구 기준

- `file-storage-module`은 파일 저장 기능 추상화 모듈이다.
- `file-storage-module`은 저장 인터페이스를 정의한다.
- `file-storage-module`은 인증이나 정책 평가를 책임지지 않는다.

## 체크리스트

- [ ] 저장/조회 추상화가 분명한가
- [ ] 벤더 종속 구현과 인터페이스가 분리되는가
- [ ] auth/audit/policy 책임과 섞이지 않았는가
- [ ] `oss-contract`의 용어와 레포 문구가 일치하는가

