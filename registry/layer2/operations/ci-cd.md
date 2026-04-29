# 2계층 CI/CD 기준

## 기본 원칙

- branch / pull request 검증은 build workflow에서 수행한다.
- publish는 tag 또는 명시적 release 흐름에서만 수행한다.
- publish job은 내부 package credential을 명시적으로 요구한다.
- 1계층 version pin 변경은 CI에서 함께 검증한다.
- local layer1 substitution은 사전 검증 옵션이며 기본 CI 경로가 아니다.

## workflow 기준

```text
.github/workflows/
  build.yml
  publish.yml
```

## build.yml 기준

- `./gradlew clean test` 또는 동등한 검증을 수행한다.
- 내부 publish credential을 요구하지 않는다.
- 필요하면 `-PuseLocalLayer1=true` 검증을 별도 job으로 둘 수 있다.

## publish.yml 기준

- internal package publish 전용이다.
- version은 tag 또는 release input에서 주입한다.
- build/test 성공 후 publish한다.
- credential 없이 실행되지 않아야 한다.
- bridge module은 module 단위 publish를 허용할 수 있다.

## 금지

- branch push에서 publish 수행
- default CI에서 local layer1 source에만 의존
- publish credential을 일반 build job에 요구
- workflow에 소비자별 배포 정책 섞기
