# 궁금했지만 항상 그냥 지나쳤던 Gradle, 얉게 한번 파보자. ~~사실 별로 궁금해하지 않고 그냥 씀~~

## Gradle? 그래들? 그레이들?
- 책에는 ‘그레이들’로 발음하는 경우가 많음
- 어차피 한글로 구글링해도 gradle로 검색됨
- 결론: 그래-들
- 빌드 자동화 툴 (친구들: ant, maven)

## 빌드란?
- 내가 작성한 코드를
- apk(`a`ndroid `p`ac`k`age), aar(`a`ndroid `ar`chive)
- 로 만드는 과정

## 안드로이드 기본 프로젝트 모양을 살펴보자
- build.gradle (Project: MyAppliation)
```
buildscript {
    repositories {
        jcenter() // mavenCentral()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.3.0'
    }
}

allprojects {
    repositories {
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```
- build.gradle (Module: app)

```
apply plugin: 'com.android.application'

android {
    compileSdkVersion 25
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "com.example.ragu.myapplication"
        minSdkVersion 19
        targetSdkVersion 25
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    compile 'com.android.support:appcompat-v7:25.1.0'
    testCompile 'junit:junit:4.12'
}

```
- gradle.settings
```
include ':app'
```
- gradle.properties
```
systemProp.http.proxyHost=70.10.15.10
systemProp.http.proxyPort=8080
systemProp.http.nonProxyHosts=70.*|localhost
 
systemProp.https.proxyHost=70.10.15.10
systemProp.https.proxyPort=8080
systemProp.https.nonProxyHosts=70.*|localhost
```

## 저장소 비교
저장소 이름|운영사|속도|규모|안드로이드 스튜디오 기본 저장소|사용자 친화도
-|-|-|-|-|-
jcenter|bintray.com|빠름(CDN 사용)|더큼|현재|높음(쉬움)
manveCentral|sonatype.org|덜빠름|큼|과거|낮음(어려움)

> bintray.com은 `jcenter`에서 `maven central`으로 배포하는 기능을 제공한다.

## gradle은 그루비로 작성되어 있다.
> Groovy is an agile and dynamic language for the Java Virtual Machine.

### 그루비란?
Groovy는 자바에 파이썬, 루비, 스몰토크등의 특징을 더한 동적 객체 지향 프로그래밍 언어입니다.  JVM에서 동작하고 자바의 강점 위에서 파이썬, 루비, 스몰토크 등의 프로그래밍 언어에 영향을 받은 특징 및 장점이 있습니다. 자바 기반이기 때문에 자바 프로그래머들이 많은 학습을 하지 않아도 프로그래밍을 할 수 있다는 점과 단순화된 문법을 지원하여 코드를 읽고 유지보수하기 편하다는 장점이 있습니다. by [불곰 블로그](http://brownbears.tistory.com)