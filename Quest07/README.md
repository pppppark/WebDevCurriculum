# Quest 07. node.js의 기초

## Introduction

- 이번 퀘스트에서는 node.js의 기본적인 구조와 개념에 대해 알아 보겠습니다.

## Topics

- node.js
- npm
- CommonJS와 ES Modules

## Resources

- [About node.js](https://nodejs.org/ko/about/)
- [Node.js의 아키텍쳐](https://edu.goorm.io/learn/lecture/557/%ED%95%9C-%EB%88%88%EC%97%90-%EB%81%9D%EB%82%B4%EB%8A%94-node-js/lesson/174356/node-js%EC%9D%98-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90)
- [npm](https://docs.npmjs.com/about-npm)
- [npm CLI commands](https://docs.npmjs.com/cli/v7/commands)
- [npm - package.json](https://docs.npmjs.com/cli/v7/configuring-npm/package-json)
- [How NodeJS Require works!](https://www.thirdrocktechkno.com/blog/how-nodejs-require-works)
- [MDN - JavaScript Modules](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Modules)
- [ES modules: A cartoon deep-dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)
- [require vs import](https://www.geeksforgeeks.org/difference-between-node-js-require-and-es6-import-and-export/)

## Checklist

- node.js는 무엇인가요? node.js의 내부는 어떻게 구성되어 있을까요?
  Node.js는 Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임이다. Node.js는 브라우저에서 JavaScript를 실행하는 것 외에도, 서버 측 애플리케이션 개발을 위해 설계되었다. Node.js는 이벤트 기반(non-blocking I/O) 및 비동기 프로그래밍 모델을 사용하여 높은 성능과 확장성을 제공한다.

  1. V8 엔진: Node.js는 Chrome 브라우저에서 사용하는 V8 엔진을 사용한다. V8 엔진은 JavaScript 코드를 컴파일하여 기계어로 변환하고 실행한다.
  2. 라이브러리: Node.js는 빌트인 모듈과 외부 패키지를 통해 다양한 기능을 제공한다. 빌트인 모듈에는 파일 시스템, HTTP, HTTPS, DNS 등이 포함되어 있으며, 외부 패키지는 npm(Node Package Manager)을 통해 설치할 수 있다.
  3. 이벤트 루프: Node.js는 이벤트 기반(non-blocking I/O) 모델을 사용하여 작업을 처리한다. 이벤트 루프는 이벤트 큐에 들어온 작업을 순서대로 처리하며, 작업이 완료될 때마다 콜백 함수를 호출한다.

  Node.js는 높은 성능과 확장성을 제공하며, JavaScript를 사용하여 서버 측 애플리케이션을 개발할 수 있도록 도와준다.

- npm이 무엇인가요? `package.json` 파일은 어떤 필드들로 구성되어 있나요?
  npm(Node Package Manager)은 node.js에서 사용할 수 있는 패키지(라이브러리)를 관리하는 도구입니다. npm을 통해 패키지를 설치하고 관리할 수 있다.
  package.json 파일은 프로젝트의 메타데이터를 포함하는 파일이다. 이 파일에는 프로젝트의 이름, 버전, 작성자, 의존성 등과 같은 정보가 포함된다. package.json 파일은 npm을 사용하여 패키지를 설치할 때 필요한 정보를 제공하고, 프로젝트의 의존성을 관리하는 데 사용된다. package.json 파일의 구성은 다음과 같다.

  name: 패키지의 이름을 정의
  version: 패키지의 버전을 정의
  description: 패키지에 대한 간단한 설명을 정의
  main: 패키지의 메인 파일을 지정
  scripts: 프로젝트에서 사용할 수 있는 스크립트를 정의
  dependencies: 패키지가 의존하는 다른 패키지의 목록을 정의
  devDependencies: 패키지를 개발할 때만 필요한 의존성 패키지를 정의
  keywords: 패키지를 검색하는 데 사용될 키워드를 정의
  license: 패키지의 라이선스를 정의
  repository: 패키지의 저장소 위치를 정의
  author: 패키지의 작성자 정보를 정의
  contributors: 패키지에 기여한 사람들의 정보를 정의
  engines: 패키지가 실행될 node.js의 최소 버전을 정의

- npx는 어떤 명령인가요? npm 패키지를 `-g` 옵션을 통해 글로벌로 저장하는 것과 그렇지 않은 것은 어떻게 다른가요?
  npx는 Node.js 패키지 매니저인 npm의 일부로, 로컬에 설치되어 있는 패키지를 실행하거나, 로컬에 설치하지 않고 실행 가능한 패키지를 일시적으로 다운로드하여 실행할 수 있게 해주는 명령어다.
  npm 패키지를 -g 옵션을 통해 글로벌로 저장하면, 해당 패키지를 전역에서 사용할 수 있게 된다. 하지만 이는 모든 프로젝트에서 사용하지 않는 패키지들까지 전역에 설치하게 되어 불필요한 용량을 차지하고, 버전 충돌 등의 문제가 발생할 수 있다. 반면에 로컬 프로젝트 내에 패키지를 설치하면 해당 프로젝트에서만 사용 가능하고, 필요할 때마다 프로젝트 내에서 패키지를 설치하여 사용할 수 있다.
  따라서 npx는 글로벌로 설치하지 않고 필요할 때마다 패키지를 다운로드하여 사용하는 것이 좋다. 이를 통해 패키지의 용량 문제와 버전 충돌 문제를 예방할 수 있다.

- 자바스크립트 코드에서 다른 파일의 코드를 부르는 시도들은 지금까지 어떤 것이 있었을까요? CommonJS 대신 ES Modules가 등장한 이유는 무엇일까요?
  ES Modules가 등장한 이유는 브라우저에서도 자바스크립트 모듈을 지원하고 있기 때문이다. 브라우저에서도 모듈을 사용할 수 있게 되면서, ES Modules가 CommonJS보다 더 일관적인 모듈 시스템을 제공하고, 브라우저에서도 동작할 수 있도록 설계되어 있기 때문에 선택할 수 있는 옵션이 늘어났다.
  이전에는 브라우저에서 자바스크립트 모듈을 사용하려면, AMD나 RequireJS 같은 라이브러리를 사용해야 했다. 또한, Node.js에서는 CommonJS 모듈 시스템을 사용해 왔다. 이 시스템에서는 require() 함수로 모듈을 로드하고, module.exports 또는 exports 객체로 모듈을 내보낸다.
  하지만 CommonJS 모듈 시스템은 동기적으로 로딩하고, 런타임에서 모듈을 동적으로 로딩하는 기능이 없기 때문에, 브라우저에서는 사용할 수 없다. 브라우저에서 AMD와 RequireJS 같은 라이브러리를 사용하면, 비동기적으로 모듈을 로딩할 수 있지만, 이들은 별도의 라이브러리를 사용해야 하기 때문에 복잡도가 증가한다.
  ES Modules는 이러한 문제를 해결하기 위해 설계된 모듈 시스템이다. ES Modules에서는 import 문으로 모듈을 로드하고, export 문으로 모듈을 내보낸다. 또한, 모듈은 비동기적으로 로딩될 수 있도록 설계되어 있다. 이러한 특징들로 인해, ES Modules는 자바스크립트 생태계에서 표준적인 모듈 시스템으로 자리 잡게 되었다.

- ES Modules는 기존의 `require()`와 동작상에 어떤 차이가 있을까요? CommonJS는 할 수 있으나 ES Modules가 할 수 없는 일에는 어떤 것이 있을까요?
  ES Modules와 require()는 모듈 시스템에 대한 두 가지 서로 다른 접근법이다. ES Modules는 자바스크립트 언어 자체에 내장되어 있으며, import와 export 키워드를 사용하여 모듈을 가져오고 내보낸다. 반면 require()는 Node.js의 일부이며, Node.js 환경에서 파일을 로드하고 모듈을 가져오는 데 사용된다.
  ES Modules와 CommonJS의 가장 큰 차이점 중 하나는 동기/비동기 로드 방식이다. ES Modules는 동기 로드를 기본으로 하며, import된 모듈은 현재 모듈이 완전히 로드되기 전까지 실행되지 않는다. 반면 CommonJS의 require()는 비동기적으로 모듈을 로드하며, 로드가 완료될 때까지 기다리지 않고 다른 코드를 실행한다. 따라서 CommonJS의 경우 콜백 함수나 Promise를 사용하여 로드가 완료된 후에 실행되어야 하는 코드를 처리해야 한다.
  ES Modules는 또한 CommonJS에서 지원하는 일부 기능을 지원하지 않는다. 가장 대표적인 예는 동적 로딩(dynamic loading)이다. CommonJS에서는 require()를 사용하여 런타임 중에 모듈을 동적으로 로드할 수 있지만, ES Modules에서는 import()를 사용하여 비동기적으로 모듈을 로드할 수는 있지만 동적으로 로드할 수는 없다.
  또한 ES Modules는 브라우저에서도 지원되는 표준 모듈 시스템이다. 이는 Node.js 모듈을 브라우저에서 사용할 수 있게 되었으며, Node.js 환경과 브라우저 환경 간의 코드 호환성을 향상시켰다. 반면 CommonJS는 Node.js에서만 지원되며 브라우저에서는 별도의 라이브러리를 사용하여야 한다.

- node.js에서 ES Modules를 사용하려면 어떻게 해야 할까요? ES Modules 기반의 코드에서 CommonJS 기반의 패키지를 불러오려면 어떻게 해야 할까요? 그 반대는 어떻게 될까요?
  mjs 확장자를 가진 파일은 기본적으로 ES Modules로 구분된다. ES Modules 기반의 코드를 작성하고 실행하려면 mjs 확장자를 사용하여 파일을 생성하고, import 구문을 사용하여 모듈을 가져와야 한다. 예를 들어, 다음과 같은 example.mjs 파일이 있다고 생각하면

  // example.mjs
  import { a } from './a.mjs';
  console.log(a());

  a.mjs 파일에서 a 함수를 정의

  // a.mjs
  export function a() {
  return 'Hello, world!';
  }

  위의 코드에서 import 구문을 사용하여 a.mjs 모듈을 가져오고, a 함수를 호출하여 출력한다.
  ES Modules 기반의 코드에서 CommonJS 기반의 패키지를 불러오려면 import 구문 대신 require 함수를 사용해야 한다. 예를 들어, example.mjs에서 express 모듈을 가져오면

  // example.mjs
  const express = require('express');
  const app = express();
  app.listen(3000, () => console.log('Server is running on port 3000'));

  하지만, 반대로 CommonJS 기반의 코드에서 ES Modules 기반의 모듈을 불러오는 것은 불가능하다. ES Modules를 사용하는 경우, import 구문을 사용하여 모듈을 가져와야한다.

## Quest

- 스켈레톤 코드에는 다음과 같은 네 개의 패키지가 있으며, 용도는 다음과 같습니다:
  - `cjs-package`: CommonJS 기반의 패키지입니다. 다른 코드가 이 패키지의 함수와 내용을 참조하게 됩니다.
  - `esm-package`: ES Modules 기반의 패키지입니다. 다른 코드가 이 패키지의 함수와 내용을 참조하게 됩니다.
  - `cjs-my-project`: `cjs-package`와 `esm-package`에 모두 의존하는, CommonJS 기반의 프로젝트입니다.
  - `esm-my-project`: `cjs-package`와 `esm-package`에 모두 의존하는, ES Modules 기반의 프로젝트입니다.
- 각각의 패키지의 `package.json`과 `index.js` 또는 `index.mjs` 파일을 수정하여, 각각의 `*-my-project`들이 `*-package`에 노출된 함수와 클래스를 활용할 수 있도록 만들어 보세요.

## Advanced

- node.js 외의 자바스크립트 런타임에는 어떤 것이 있을까요?
