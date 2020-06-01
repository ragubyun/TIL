# 자바스크립트 모듈 시스템 정리

> ES6 Modules vs CommonJS vs RequireJS

JavaScript는 태생적인 한계로 인해 자체 모듈 관리 기능이 없었다.(ES6 이전)

이후 ES6에서 자체 모듈 관리 기능을 추가하였으나, 아직 모든 브라우저에서 ES6의 모듈을 지원하지 않고 있어서 CommonJS, RequireJS 등과 같은 모듈 로더 또는 webpack, parcel, snowpack 등과 같은 모듈 번들러를 사용해야 한다.

## 1. ES6 Modules(ESM) - ES6에서 추가된 모듈 기능

- `export`, `import` 키워드 사용
- `동기적` 모듈 정의
- 클라이언트, 서버사이드에서 모두 동작
- IE 미지원
- 몇가지 이슈가 있었지만 현재(2020. 04.) 거의 다 해결됨

## 2. CommonJS - de facto standard

- `require`, `exports` 키워드 사용
- `동기적` 모듈 정의
- Node.js에서 채택
- 브라우저 밖에서의 실행에 중점

### 2-1. Node.js Module System - CommonJS의 구현체

- `require`, `module.exports` 키워드 사용
- `require`를 통해 `node_modules` 디렉토리 안의 모듈 이름을 체크
- CommonJS를 채택하였으나 현재 사양이 100% 동일하진 않음.

## 3. AMD(Asynchronous Module Definition)

- `비동기적` 모듈 정의
- 모듈 로딩이 끝나면 callback 함수가 호출됨
- 브라우저 내에서의 실행에 중점

### 3-1. RequireJS - AMD의 구현체

- JavaScript Module Loader
- 동적 모듈 로딩
- CommonJS 스타일의 포맷도 지원
- 깔끔한 API와 문서
