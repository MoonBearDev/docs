---
sidebar_position: 1
---

# 시작하기

![Android](https://img.shields.io/badge/Daro_Android_SDK-v0.6.3-3DDC84?logo=android&logoColor=white)

Daro Android SDK를 앱에 통합하는 방법에 대해 안내합니다.

---

## 시작하기 전에

프로젝트에 Daro SDK를 통합하기 전에 필요한 사항들을 확인하세요.

### 요구사항

- 안드로이드 minSdkVersion : 24

### 안내사항

- AdMob 자체 이슈로 인하여 Banner와 Native 광고를 Jetpack Compose 위에 올릴 경우, impression이 정상적으로 집계되지 않아 수익에 악영향이 있습니다.
  - Banner와 Native 광고는 기존 안드로이드 뷰 방식위에 올려주세요.
  - Jetpack Compose의 [AndroidView Composable](<https://developer.android.com/reference/kotlin/androidx/compose/ui/viewinterop/package-summary?_gl=1*sfjhoo*_up*MQ..*_ga*MTc5NjYzMDU3Ni4xNzE1MjI4ODQy*_ga_6HH9YJMN9M*MTcxNTIyODg0MS4xLjAuMTcxNTIyODg0MS4wLjAuMA..#AndroidView(kotlin.Function1,androidx.compose.ui.Modifier,kotlin.Function1)>) 역시 같은 이슈가 존재합니다.

---

## 앱 설정하기

### 프로젝트 단위 빌드 설정

1. gradle.properties 파일에 아래 설정을 추가합니다.

   ```xml
   android.useAndroidX=true
   android.enableJetifier=true
   ```

2. settings.gradle 파일에 maven repository 들을 추가합니다.
   - build.gradle.kotlin (Kotlin)
     ```kotlin
     dependencyResolutionManagement {
         ...
         repositories {
             google()
             mavenCentral()
             ...
             maven {
                 url = uri("https://jitpack.io")
             }
             maven {
                 url = uri("https://artifact.bytedance.com/repository/pangle")
             }
             maven {
                 url = uri("https://verve.jfrog.io/artifactory/verve-gradle-release")
             }
             maven {
                 url = uri("https://cboost.jfrog.io/artifactory/chartboost-ads/")
             }
             maven {
                 url = uri("https://repo.premiumads.net/artifactory/mobile-ads-sdk/")
             }
             maven {
                 url = uri("https://repo.pubmatic.com/artifactory/public-repos")
             }
             maven {
                 url = uri("https://s3.amazonaws.com/smaato-sdk-releases/")
             }
             maven {
                 url = uri("https://android-sdk.is.com/")
             }
             maven {
                 url = uri("https://dl-maven-android.mintegral.com/repository/mbridge_android_sdk_oversea")
             }
         }
     }
     ```
   - build.gradle (Groovy)
     ```groovy
     allprojects {
         ...
         repositories {
             ...
             maven {
                 url "https://jitpack.io"
             }
             maven {
                 url "https://artifact.bytedance.com/repository/pangle"
             }
             maven {
                 url "https://verve.jfrog.io/artifactory/verve-gradle-release"
             }
             maven {
                 url "https://cboost.jfrog.io/artifactory/chartboost-ads/"
             }
             maven {
                 url "https://repo.premiumads.net/artifactory/mobile-ads-sdk/"
             }
             maven {
                 url "https://repo.pubmatic.com/artifactory/public-repos"
             }
             maven {
                 url "https://s3.amazonaws.com/smaato-sdk-releases/"
             }
             maven {
                 url "https://android-sdk.is.com/"
             }
             maven {
                 url "https://dl-maven-android.mintegral.com/repository/mbridge_android_sdk_oversea"
             }
         }
     ```
3. build.gradle(root) 파일에 buildScript를 추가합니다.

   - build.gradle (Groovy)

     ```groovy
     buildscript {
         repositories {
             google()
             mavenCentral()
             maven { url "https://jitpack.io" }
         }
         dependencies {
             classpath 'com.github.delightroom:daro-android-plugin:0.3.0'
         }
     }
     ```

   - build.gradle.kotlin (Kotlin)

     ```kotlin
     buildscript {
         repositories {
             google()
             mavenCentral()
             maven { url = uri("https://jitpack.io") }
         }
         dependencies {
             classpath("com.github.delightroom:daro-android-plugin:0.3.0")
         }
     }
     ```

<br />

### 모듈 단위 빌드 설정

1. Daro SDK를 추가합니다. (latest: `0.6.3`)

   - build.gradle.kotlin (Kotlin)

   ```kotlin
   plugins {
       ...
       id("droom.daro.a")
       ...
   }

   dependencies {
       ...
       implementation("com.github.delightroom:daro-android:${version}")
       ...
   }
   ```

   - build.gradle (Groovy)

   ```groovy
   plugins {
       ...
       id 'droom.daro.a'
       ...
   }

   dependencies {
       ...
       implementation 'com.github.delightroom:daro-android:${version}'
       ...
   }
   ```

2. rootProject에 daro-service.json 파일을 추가합니다.

   ```
   ${rootProject}/
   ├── app/
   │
   ...
   │
   ├── daro-serivce.json

   ```

   :::note
   `daro-service.json` 파일은 DARO 대시보드에서 앱을 등록하고 앱 리스트 표의 맨 오른쪽 Key File 열에서 Download 버튼 클릭하여 다운로드 받을 수 있습니다.
   :::

---

## SDK 초기화하기

```kotlin
import android.app.Application
import droom.daro.lib.Daro
import droom.daro.lib.DaroNetworkConfiguration
import droom.daro.lib.util.logger.DaroLogLevel
import kotlinx.coroutines.CoroutineScope

class SampleApp: Application() {

        override fun onCreate() {
        super.onCreate()

        CoroutinScope.launch {
            Daro.init(
                application = this@SampleApp,
            )
        }
    }
}
```

💡 빠른 SDK 초기화를 위해 앱의 첫 진입점인 Application 파일 onCreate 내에서 Daro SDK를 초기화하는 것을 권장합니다.

<br />
