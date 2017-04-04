# 안드로이드에서 자바8 기능 사용하기 위한 세팅(람다)

- jdk 1.8 설치

- 프로젝트 수준의 build.gradle에 아래 내용 추가

```gradle
apply plugin: 'me.tatarka.retrolambda' // Retrolambda 플러그인 사용

buildscript {
    dependencies {
        ...
        classpath 'me.tatarka:gradle-retrolambda:3.6.0'
    }
}
```

- 모듈 수준의 build.gradle에 아래 내용을 추가

```gradle
android {
  ...
  defaultConfig {
    ...
    jackOptions {
      enabled true
    }
  }
  compileOptions {
    sourceCompatibility JavaVersion.VERSION_1_8
    targetCompatibility JavaVersion.VERSION_1_8
  }
}
```

> **참고:** 안드로이드에서 자바8 기능을 사용하려면 [Jack](https://source.android.com/source/jack.html?hl=ko)이라는 컴파일러가 필요하다.

java, jack 툴체인 비교

- 레거시 javac 툴체인

  javac(.java → .class) → dx (.class → .dex)

- 새로운 Jack 툴체인

  Jack(.java → .jack → .dex)
