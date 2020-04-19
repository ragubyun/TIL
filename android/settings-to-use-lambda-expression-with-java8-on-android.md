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

> **참고** 안드로이드에서 자바8 기능을 사용하려면 [Jack](https://source.android.com/source/jack.html?hl=ko)이라는 컴파일러가 필요하다.

> **추가1** retrolambda를 사용하면 jack 툴체인을 쓰지 않고 컴파일이 가능하기 때문에 `jackOptions`을 활성화 시키지 않아도 된다.

> **추가2** retrolambda를 사용하지않고 jack 툴체인을 써서 Java8의 람다식을 사용할 수도 있으나, 테스트 코드를 짜는데 문제가 있어서 아직까지는 retrolambda를 써야 할 듯. (robolectric에서 오류 뱉음)

java, jack 툴체인 비교

- 레거시 javac 툴체인

  javac(.java → .class) → dx (.class → .dex)

- 새로운 Jack 툴체인

  Jack(.java → .jack → .dex)
