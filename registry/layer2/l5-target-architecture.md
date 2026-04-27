# L5 목표 구조

이 문서는 1계층 OSS 모듈, 2계층 플랫폼 4개, 3계층 서비스 레포로 정리하는 최종 목표 구조를 설명한다.

현재 구현 상태를 그대로 설명하는 문서가 아니다.
한 번에 구조를 재편할 때 어떤 책임을 어디에 두는지가 이 문서의 목적이다.

## 한 줄 정의

- OSS는 기능 부품이다.
- Platform은 회사 표준 실행 흐름이다.
- Service는 도메인 로직만 가진다.

즉 서비스는 OSS를 직접 보지 않고, 플랫폼만 소비한다.

## 전체 구조

```text
3계층 서비스 레포
service-gateway
service-auth
service-user
service-authz
service-editor
service-redis

        ↓ consumes

2계층 플랫폼
platform-security
platform-governance
platform-resource
platform-integrations

        ↓ wraps / standardizes

1계층 OSS
oss-auth
oss-ip-guard
oss-audit-log
oss-rate-limiter
oss-policy-config
oss-plugin-policy-engine
oss-file-storage
oss-notification
```

## 핵심 원칙

- 서비스는 비즈니스 도메인을 소유한다.
- 플랫폼은 반복되는 인프라 실행 흐름을 소유한다.
- OSS는 플랫폼 내부 구현 부품으로만 소비한다.
- 서비스는 OSS 타입, OSS SPI, OSS 내부 구현을 직접 알면 안 된다.
- 서비스에는 설정, 플랫폼 SPI 구현, 도메인 연결 코드만 남겨야 한다.

## 플랫폼 4개

### 1. `platform-security`

역할:
인증, 인가, 토큰, 세션, 보안 필터의 표준 실행 플랫폼

소유해야 할 것:
- 인증 필터 체인
- 로그인 파이프라인
- JWT 발급과 검증
- refresh token 정책
- logout 처리
- 인증 실패 응답 표준화
- SecurityContext 구성
- 인증 이벤트 발행
- 권한 검증 진입점

주로 소비하는 OSS:
- `oss-auth`
- `oss-ip-guard`
- `oss-rate-limiter`

서비스가 해야 하는 것:
- `service-auth`의 `AuthUserProvider` 구현
- credential 저장소 연결
- user 상태 조회 연결
- refresh token 저장소 SPI 구현
- `application.yml` 설정

서비스가 하지 말아야 하는 것:
- 직접 JWT 발급
- 직접 로그인 컨트롤러 핵심 로직 구현
- 직접 인증 필터 구현
- 직접 보안 예외 응답 포맷 구현

### 2. `platform-governance`

역할:
감사, 정책, 운영 통제 표준 플랫폼

소유해야 할 것:
- audit event 표준 모델
- audit sink 표준화
- policy config 로딩
- plugin policy engine 실행
- 운영 정책 평가 결과 표준화
- 위반 대응 handler
- 보안/운영 이벤트 기록 기준

주로 소비하는 OSS:
- `oss-audit-log`
- `oss-policy-config`
- `oss-plugin-policy-engine`

서비스가 해야 하는 것:
- 어떤 행위가 감사 대상인지 선언
- 어떤 endpoint나 use case에 어떤 정책을 붙일지 선언
- 도메인 이벤트에 audit context 제공

서비스가 하지 말아야 하는 것:
- 직접 audit log 포맷 정의
- 직접 정책 엔진 호출 구조를 매번 작성
- 직접 운영 판단 결과 모델을 서비스마다 따로 정의

주의:
`platform-governance`는 정책과 운영 기준의 owner다.
요청을 실제로 차단하거나 인증 흐름에서 집행하는 책임은 `platform-security`에 둔다.

### 3. `platform-resource`

역할:
파일, 첨부, 이미지, 저장소 접근을 공통 방식으로 다루는 리소스 플랫폼

소유해야 할 것:
- 파일 업로드, 다운로드, 삭제 공통 흐름
- presigned URL 발급
- 파일 크기, 확장자, MIME 정책
- 저장 경로 규칙
- 파일 메타데이터 표준 모델
- resource owner, kind, access, lifecycle
- 스토리지 provider 추상화

주로 소비하는 OSS:
- `oss-file-storage`
- `oss-notification`

서비스가 해야 하는 것:
- 문서 첨부파일과 도메인 연결
- block image/file metadata 저장
- `resourceId`를 도메인 엔티티에 연결
- 프로필 이미지 같은 도메인 리소스와 서비스 API 연결

서비스가 하지 말아야 하는 것:
- 직접 S3 SDK 호출
- 직접 파일 검증 로직 구현
- 직접 presigned URL 발급
- 서비스마다 다른 파일 경로 규칙 사용

주의:
`platform-resource`는 단순 파일 유틸이 아니다.
저장만이 아니라 resource lifecycle 전체를 표준화하는 계층으로 본다.

### 4. `platform-integrations`

역할:
알림, 외부 시스템 연동, 메시지 발행 같은 outbound 실행 표준 플랫폼

소유해야 할 것:
- notification 표준 모델
- email, SMS, push, webhook provider 추상화
- 알림 템플릿 처리
- 발송 실패 재시도 정책
- 외부 연동 예외 표준화
- integration event 발행
- idempotency key 처리

주로 소비하는 OSS:
- `oss-notification`

서비스가 해야 하는 것:
- 비밀번호 재설정 알림 요청
- 로그인 보안 알림 요청
- 가입, 프로필 변경 알림 요청
- 문서 공유, 댓글, 협업 알림 요청

서비스가 하지 말아야 하는 것:
- 직접 메일 발송 구현
- 직접 SMS provider 호출
- 직접 알림 재시도 로직 구현
- 서비스마다 알림 포맷 따로 정의

주의:
이 플랫폼은 outbound 실행 표준을 소유해야 한다.
도메인별 메시지 의미와 발송 타이밍은 서비스가 결정한다.

## 플랫폼 간 관계

권장 구조는 수평 독립과 최소 의존이다.

좋은 방향:

```text
platform-security     -> platform-governance
platform-resource     -> platform-governance
platform-integrations -> platform-governance
```

피해야 할 구조:

```text
platform-security <-> platform-governance
platform-resource <-> platform-integrations
```

## 서비스 레포의 최종 모습

- `service-auth`: 사용자 조회, token store, 설정
- `service-user`: user와 profile 도메인
- `service-editor`: document와 resource 연결, audit context
- `service-gateway`: route와 ingress 설정

## 최종 정리

- `platform-security` = 인증과 인가 실행 플랫폼
- `platform-governance` = 감사와 정책과 운영 통제 플랫폼
- `platform-resource` = 파일과 리소스 lifecycle 플랫폼
- `platform-integrations` = 알림과 외부 연동 outbound 플랫폼
