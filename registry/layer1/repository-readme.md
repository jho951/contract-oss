# README.md 기준 - 1계층 OSS

1계층 OSS 레포의 `README.md`는 소비자가 빠르게 공개 좌표, 책임, 제외 범위, 문서 위치를 확인할 수 있어야 한다.

## 목표 구조

```md
# <repo-name>

`<repo-name>`는 `<role-summary>` 책임을 가진 1계층 OSS다.

## 공개 좌표

- `io.github.jho951:<artifact-1>`
- `io.github.jho951:<artifact-2>`

## 무엇을 제공하나

- `<module-1>`: `<role>`
- `<module-2>`: `<role>`

## 책임 경계

포함한다:

- `<included-responsibility-1>`
- `<included-responsibility-2>`

포함하지 않는다:

- platform 조립 책임
- 서비스 비즈니스 로직
- 도메인 권한 판단
- framework integration이 해당 레포 책임이 아닌 경우 그 책임

## 빠른 시작

```gradle
repositories {
    mavenCentral()
}

dependencies {
    implementation("io.github.jho951:<artifact>:<version>")
}
```

## 문서

- [docs/README.md](docs/README.md)
```

## 작성 기준

- 공개 좌표는 실제 Maven Central publish artifact와 일치해야 한다.
- `무엇을 제공하나`는 `settings.gradle` include 목록과 일치해야 한다.
- 책임 경계에는 1계층 책임과 2계층 platform 책임을 명확히 나눈다.
- `CONTRACT_SYNC.md` 같은 SOT 내부 문서를 레포 README에 안내하지 않는다.
- badge는 허용하되, 버전/좌표/문서 링크를 가리지 않아야 한다.
