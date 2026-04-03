# rate-limiter docs

이 문서는 `platform-security`의 `rate-limiter` 구현 레포 문서를 정리한다.

## 기준

- 공개 계약 기준: `oss-contract`
- 실제 서비스 계약 기준: `service-contract`

## 범위

- 요청 속도 제한
- IP / 사용자 ID / API 키 기준 제한
- in-memory / Redis / Spring Boot 연동

## 범위 밖

- 인증 principal
- 정책 엔진
- 감사 저장
- 파일 저장

