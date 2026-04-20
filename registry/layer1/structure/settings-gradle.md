# settings.gradle 구조 기준 - 1계층 OSS

1계층 OSS 레포는 `settings.gradle`에서 root project, publish aggregation, 공개 모듈 include를 명확히 고정한다.

## 공통 구조

```groovy
plugins {
    id 'com.gradleup.nmcp.settings' version '<nmcp-version>'
}

def optionalSettingProp = { String envName, String propKey ->
    def envValue = System.getenv(envName)?.trim()
    envValue ?: providers.gradleProperty(propKey).orNull?.trim()
}

nmcpSettings {
    centralPortal {
        username = optionalSettingProp('MAVEN_CENTRAL_USERNAME', 'mavenCentralUsername')
        password = optionalSettingProp('MAVEN_CENTRAL_PASSWORD', 'mavenCentralPassword')
        publishingType = 'AUTOMATIC'
    }
}

rootProject.name = '<repo-name>'

include '<published-module-1>'
include '<published-module-2>'
```

## include 기준

- `include` 목록은 publish 대상 모듈과 일치해야 한다.
- README의 공개 좌표와 `docs/modules.md`의 모듈 목록도 같은 목록을 써야 한다.
- Spring/starter/platform 조립 모듈은 1계층 OSS 기본 include 대상으로 두지 않는다.
- 실험 모듈, 샘플 모듈, 생성 산출물은 publish include에 섞지 않는다.

## 최신 tag 기준 모듈 예시

- `auth`: `auth-core`, `auth-jwt`, `auth-session`, `auth-hybrid`, `auth-apikey`, `auth-hmac`, `auth-oidc`, `auth-service-account`
- `ip-guard`: `ip-guard-core`, `ip-guard-spi`
- `rate-limiter`: `rate-limiter-core`, `rate-limiter-spi`
- `audit-log`: `audit-log-api`, `audit-log-core`
- `policy-config`: `policy-config-contracts`, `policy-config-core`, `policy-config-builder`
- `plugin-policy-engine`: `plugin-policy-engine-api`, `plugin-policy-engine-core`, `plugin-policy-engine-config`
- `file-storage`: `file-storage-api`, `file-storage-core`
- `notification`: `notification-api`, `notification-core`

## 규칙

- `com.gradleup.nmcp.settings`를 settings 레벨에 둔다.
- Central Portal credential은 property 또는 environment variable로 주입한다.
- `publishingType = 'AUTOMATIC'`을 사용한다.
- 모듈 목록 변경은 README, docs, repository catalog와 같이 맞춘다.
