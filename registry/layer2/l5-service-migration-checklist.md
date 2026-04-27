# L5 서비스별 마이그레이션 체크리스트

이 문서는 [l5-target-architecture.md](l5-target-architecture.md)와 [l5-migration-plan.md](l5-migration-plan.md)을 서비스 레포 단위로 풀어쓴 실행 체크리스트다.

목적은 간단하다.
각 서비스가 무엇을 계속 소유하고, 무엇을 플랫폼으로 올리고, 무엇을 지워야 하는지를 바로 판단하게 하는 것이다.

## 공통 체크

모든 서비스는 아래 질문에 `예`라고 답할 수 있어야 한다.

- OSS 타입을 직접 import하지 않는가
- platform starter, platform API, platform SPI만 보고 있는가
- 인증, 감사, 파일, 알림 실행 흐름을 서비스가 직접 구현하지 않는가
- 서비스 코드는 도메인 모델, 도메인 규칙, 플랫폼 연결 코드 위주로 남아 있는가
- 서비스별 helper, util, formatter, sender, filter가 플랫폼으로 올라갔는가

## `service-gateway`

### 서비스가 계속 소유할 것

- route와 ingress 구성
- 공개 endpoint 배치
- 외부 노출 정책 연결
- 서비스별 edge 설정

### 플랫폼으로 올릴 것

- 인증 필터 체인
- JWT 검증 진입점
- ingress rate limit 집행
- IP 제한 집행
- 차단 응답 포맷
- 감사/정책 기준 연결

### 삭제 후보

- gateway 내부 JWT helper
- gateway 내부 rate-limit helper
- gateway 내부 IP block helper
- gateway 내부 security exception formatter

### 완료 기준

- gateway는 `platform-security`와 `platform-governance` 설정만 붙인다.
- gateway는 raw OSS 보안 타입을 직접 import하지 않는다.

## `service-auth`

### 서비스가 계속 소유할 것

- 사용자 조회
- credential 저장소 연결
- user 상태 확인
- refresh token 저장소 구현
- 비밀번호 재설정, 계정 잠금 같은 인증 도메인 규칙

### 플랫폼으로 올릴 것

- 로그인 파이프라인
- JWT 발급과 검증
- logout 공통 흐름
- 인증 실패 응답 표준화
- SecurityContext 구성
- 로그인 보안 이벤트 발행
- 알림 발송 실행 흐름

### 삭제 후보

- service-owned login helper
- service-owned token helper
- service-owned auth filter
- service-owned mail sender
- service-owned security audit adapter

### 완료 기준

- `service-auth`는 `AuthUserProvider`, token store, user 상태 조회 구현만 남긴다.
- 메일, SMS, 보안 알림 발송은 `platform-integrations`를 통해서만 나간다.

## `service-user`

### 서비스가 계속 소유할 것

- user 도메인
- profile 도메인
- role과 status API
- 가입, 탈퇴, 프로필 변경 규칙

### 플랫폼으로 올릴 것

- 프로필 이미지 저장 흐름
- 파일 검증과 저장 규칙
- 가입/프로필 변경 알림 발송
- 관련 감사 기록 표준화

### 삭제 후보

- service-owned file upload helper
- service-owned image validation helper
- service-owned profile image storage client
- service-owned notification sender

### 완료 기준

- `service-user`는 profile image의 도메인 의미만 가진다.
- 파일 저장과 presigned URL 발급은 `platform-resource`를 통해서만 처리한다.

## `service-authz`

### 서비스가 계속 소유할 것

- 도메인 권한 규칙
- 역할, 권한, 정책 매핑의 도메인 의미
- 권한 조회 API

### 플랫폼으로 올릴 것

- 권한 검증 진입점 공통화
- 정책 평가 실행 흐름
- 감사 기록 표준화
- 위반 응답 표준화

### 삭제 후보

- service-owned permission evaluator wrapper
- service-owned policy engine caller
- service-owned access denied formatter

### 완료 기준

- `service-authz`는 누가 무엇을 할 수 있는지에 대한 도메인 사실만 소유한다.
- 실제 요청 차단과 정책 집행 흐름은 `platform-security`와 `platform-governance`를 통해 처리한다.

## `service-editor`

### 서비스가 계속 소유할 것

- document 도메인
- block 도메인
- 문서 공유, 댓글, 협업 규칙
- 어떤 행위가 감사 대상인지에 대한 선언

### 플랫폼으로 올릴 것

- 첨부파일 업로드, 다운로드, 삭제
- block image/file 저장 흐름
- resource metadata, owner, access, lifecycle
- 문서 관련 감사 기록 표준화
- 공유/댓글/협업 알림 발송

### 삭제 후보

- service-owned file storage helper
- service-owned S3 client wrapper
- service-owned audit formatter
- service-owned collaboration sender

### 완료 기준

- `service-editor`는 `resourceId`와 document/block 도메인 연결만 가진다.
- 첨부파일 저장과 외부 알림 발송은 각각 `platform-resource`, `platform-integrations`로 분리된다.

## `service-redis`

### 서비스가 계속 소유할 것

- Redis 운영 역할이 정말 서비스 레포로 필요한지 판단
- 캐시 키의 도메인 의미
- 캐시 만료 정책의 비즈니스 의미

### 플랫폼으로 올릴 것

- 인증 세션 저장 규칙
- refresh token 저장 공통화
- rate-limit 저장소 연결
- idempotency 저장소 연결

### 삭제 후보

- 플랫폼 기능을 대신하는 범용 Redis helper
- 서비스마다 다른 key naming convention 유틸
- 보안, 알림, 리소스 저장을 뒤섞은 공용 Redis adapter

### 완료 기준

- `service-redis`가 남는다면 도메인 캐시나 운영 저장소처럼 이유가 분명해야 한다.
- 보안, 알림, 리소스 플랫폼이 필요한 Redis 사용은 각 플랫폼 contract 뒤로 숨긴다.

## 서비스별 최종 모습

최종적으로 서비스 레포는 아래처럼 얇아져야 한다.

- `service-gateway`: route, ingress 설정, platform wiring
- `service-auth`: 사용자 조회, token store, 설정
- `service-user`: user/profile 도메인
- `service-authz`: 도메인 권한 의미
- `service-editor`: document/block 도메인, resource 연결
- `service-redis`: 남겨야 할 도메인 저장소가 있을 때만 제한적으로 유지

## 마지막 점검

아래 항목이 남아 있으면 아직 L5 전환이 끝난 것이 아니다.

- 서비스가 OSS 구현체를 직접 생성한다
- 서비스가 JWT, audit, file, notification helper를 직접 가진다
- 서비스가 policy engine 호출 구조를 직접 안다
- 서비스가 provider SDK를 직접 호출한다
- 플랫폼 없이도 돌아가는 중복 실행 흐름이 서비스마다 남아 있다
