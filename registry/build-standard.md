# build.gradle 표준

이 문서는 1계층 OSS 레포의 `build.gradle` 공통 표준을 정의한다.

## 기본 방향

- 1계층 OSS는 `java-library` 중심으로 만든다.
- 배포 가능한 Maven artifact를 만든다.
- 테스트와 배포 설정을 분리한다.
- 공통 버전과 publishing 규칙은 동일하게 가져간다.

## 권장 플러그인

- `java-library`
- `maven-publish`
- `signing`

## 권장 산출물

- main jar
- sources jar
- javadoc jar

## 공통 설정

- Java toolchain 버전 통일
- UTF-8 encoding 통일
- Maven Central publishing metadata 통일
- GitHub Actions에서 version 주입 가능하게 구성

## 금지 사항

- 서비스 실행용 애플리케이션 설정을 라이브러리 표준에 섞지 않는다.
- 레포별로 다른 publishing 방식은 만들지 않는다.
- tag, version, artifact naming 규칙을 제각각 두지 않는다.

