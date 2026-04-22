# 2계층 publish 기준

2계층 platform은 private package 또는 내부 배포 흐름을 전제로 한다.
공개 Maven Central 배포를 선택하더라도 build, settings, workflow 책임 분리는 동일하게 유지한다.

## 목적

- `gradle.properties`, `build.gradle`, `settings.gradle`, `publish.yml`의 책임을 분리한다.
- platform artifact version과 dependency pin을 같은 release 단위로 검증한다.
- publish credential이 일반 build 검증에 섞이지 않게 한다.
- README, usage, private-publish 같은 소비 문서가 실제 published module surface와 같이 움직이게 한다.

## gradle.properties 책임

- `release_version`: publish 시 주입되는 artifact version
- `release_group`: artifact group
- `java_version`: Java toolchain 기준
- `github_org`, `github_repo`: package metadata 조립 기준
- layer1 dependency version key: exact version pin 기준

## build.gradle 책임

- platform module publication 정의
- BOM / starter / autoconfigure / bridge artifact 분리
- 공개 시그니처가 외부 타입을 노출하면 해당 의존성을 `api` 범위로 선언해 published metadata와 compile surface를 일치시킨다.
- package metadata 작성
- 내부 package 또는 공개 package repository 설정
- signing이 필요한 publish target이면 signing 설정

## settings.gradle 책임

- root project name 고정
- publish 대상 module include
- local layer1 substitution은 선택 옵션으로만 제공
- production publish는 published artifact dependency를 기준으로 수행

## publish.yml 책임

- tag 또는 명시적 release input에서만 publish한다.
- publish 전에 build/test를 수행한다.
- `release_version`을 publish 시점에 주입한다.
- 내부 package credential 또는 공개 package credential을 env로 주입한다.
- bridge module은 module 단위 publish를 허용할 수 있다.

## 필요한 secret

publish target에 따라 필요한 secret만 둔다.

- 내부 package username/token
- 공개 package username/token
- signing key/password

## 검증 항목

- `release_version`이 publish 시점에만 쓰이는가
- layer1 dependency version이 exact version으로 고정되어 있는가
- `build.gradle`이 publish 가능한 platform artifact를 만드는가
- `settings.gradle` include가 publish 대상 module과 일치하는가
- README, usage, private-publish 예시가 실제 publish된 starter/adapter/relay/module 좌표와 일치하는가
- `publish.yml`이 tag 또는 release input 기반으로만 publish하는가
- publish credential이 build workflow에 요구되지 않는가

## 금지 사항

- branch push에서 publish 수행
- publish 좌표 하드코딩
- dynamic version으로 platform publish
- default CI에서 local layer1 source에만 의존
- 생성 산출물을 publish source에 포함
