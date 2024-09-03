
932 ~ 949
https://velog.io/@qkrtofha94/%EB%AA%A8%EB%8D%98-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Deep-Dive-49%EC%9E%A5-Babel%EA%B3%BC-Webpack%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-ES6ES.NEXT-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95

49장 Babel과 Webpack을 이용한 ES6+/ES.NEXT 개발환경 구축
===
- 크롬, 사파리, 파이어 폭스 같은 에버그린 브라우저의 ES6 지원율은 약 98%로 거의 대부분의 ES6 사양을 지원한다.
  - 하지만 IE 11의 ES6 지원율은 약 11%다.
  - 그리고 매년 새롭게 도입되는 ES6 이상의 버전과 제안 단계에 있는 ES 제안 사양은 브라우저에 따라 지원율이 제각각이다.

- 따라서 ES6+와 ES.NEXT의 최신 ECMAScript 사양을 사용하여 프로젝트를 진행하려면 최신 사양으로 작성된 코드를 경우에 따라 IE를 포함한 구형 브라우저에서 문제 없이 동작시키기 위한 개발 환경을 구축하는 것이 필요하다.

- 또한 대부분의 프로젝트가 모듈을 사용하므로 모듈 로더도 필요하다.

- Babel은 트랜스파일러, Webpack은 모듈 번들러이다.

- Webpack을 통해 Babel을 로드하여 ES6+와 ES.NEXT 사양의 소스코드를 구형 브라우저에서도 동작하도록 ES5 사양의 소스코드로 트랜스파일링 할 수 있다.

Babel
---
- 아래처럼 ES6의 화살표 함수와 ES7의 지수 연산자를 사용할 때 구형 브라우저에서는 지원하지 않을 수 있으므로 Babel을 사용해 아래 코드를 ES5 사양으로 변환할 수 있다.
```
[1,2,3].map(n => n ** n);
```
```
"use strict";

[1, 2, 3].map(function (n) {
  return Math.pow(n, n);
});
```
- 이처럼 Babel은 ES6+와 ES.NEXT로 구현된 최신 사양의 소스코드를 구형 브라우저에서도 동작하는 ES5 사양의 소스코드로 변환(트랜스파일링)할 수 있다.

- Babel 설치
```
# package.json 생성
npm init -y
# babel/core, babel/cli 설치
npm install --save-dev @babel/core @babel/cli
```

- Babel 프리셋 설치와 babel.config.json 파일 작성
  - Babel을 사용하려면 @babel/preset-env를 설치해야 한다.
  - @babel/preset-env는 함께 사용되어야 하는 Babel 플러그인을 모아둔 것으로 Babel 프리셋이라고 부른다.
```
# @babel/preset-env 설치
npm install --save-dev @babel/preset-env 
```
babel.config.json
```
{
	"presets": ["@babel/preset-env"]
}
```

- 트랜스파일링
  - Babel을 사용하여 ES6+/ES.NEXT 사양의 소스코드를 ES5 사양의 소스코드로 트랜스파일링할 수 있다.
 
- Babel 플러그인 설치
```
npm install --save-dev @babel/plugin-proposal-class-properties
```

- 브라우저에서 모듈 로딩 테스트
  - 브라우저에서는 CommonJS 방식의 require 함수를 지원하지 않으므로 트랜스파일링된 결과를 그대로 브라우저에서 실행하면 에러가 발생한다.

Webpack
---
- Webpack은 의존 관계에 있는 자바스크립트, CSS, 이미지 등의 리소스들을 하나의 파일로 번들링하는 모듈 번들러다.

- Webpack을 사용하면 의존 모듈이 하나의 파일로 번들링되므로 별도의 모듈 로더가 필요없다.

- 그리고 여러 개의 자바스크립트 파일을 하나로 번들링하므로 HTML 파일에서 script 태그로 여러 개의 자바스크립트 파일을 로드해야 하는 번거로움도 사라진다.

- Webpack 설치
```npm install --save-dev webpack webpack-cli```

- babel-loader 설치
```npm install --save-dev babel-loader```

- webpack.config.js 설정 파일 작성
  - webpack.config.js는 Webpack이 실행될 때 참조하는 설정 파일이다.
 
- babel-polyfill 설치
  - babel을 사용해 소스코드를 트랜스파일링해도 브라우저가 지원하지 않는 코드가 남아 있을 수 있다.
  - Promise, Object.assign 등과 같이 ES5 사양으로 대체할 수 없는 기능은 트랜스파일링되지 않는다.
  - 따라서 구형 브라우저에서도 Promise, Object.assign 등과 같은 객체나 메서드를 사용하기 위해서는 @babel-polyfill을 설치해야 한다.
  ```npm install @babel-polyfill```
