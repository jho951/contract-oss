# Access Flow

`ip-guard`는 요청 진입 시점의 IP 판단을 담당한다.

## 흐름

1. 요청에서 client IP를 추출한다.
2. allowlist와 denylist를 조회한다.
3. 정책 소스를 기준으로 허용 여부를 계산한다.
4. 결과를 Spring 연동 계층으로 전달한다.

## 판단 기준

- denylist가 allowlist보다 우선한다.
- 요청 진입 차단은 인증보다 앞선다.
- core는 프레임워크 타입에 의존하지 않는다.

## 제외 범위

- token 발급
- principal 생성
- 정책 평가
- 감사 로그 저장
- 파일 저장
