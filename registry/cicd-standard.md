# CI/CD 표준

이 문서는 1계층 OSS 레포의 공통 CI/CD 표준을 정의한다.

## 목적

- 테스트와 배포 절차를 통일한다.
- 태그 기반 릴리즈를 표준화한다.
- GitHub Actions secret 기반 publish 흐름을 통일한다.

## 표준 흐름

1. PR에서 test / verify를 실행한다.
2. main 또는 release 브랜치에 병합한다.
3. Git tag를 생성한다.
4. GitHub Actions가 tag를 감지한다.
5. tag에서 `releaseVersion`을 추출한다.
6. Maven Central에 publish 한다.

## 필요한 secret / 설정

- Maven Central 사용자 정보
- signing key
- signing password
- repository token 또는 equivalent

## 공통 workflow 원칙

- workflow 파일 이름을 최대한 통일한다.
- publish job과 test job을 분리한다.
- tag push시에만 publish한다.
- 일반 branch push는 publish하지 않는다.
- publish job은 `-PreleaseVersion`을 전달한다.

## 검증 항목

- build 성공
- test 성공
- artifact 생성 성공
- signing 성공
- publish 성공
