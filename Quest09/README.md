# Quest 09. 서버와 클라이언트의 대화

## Introduction

- 이번 퀘스트에서는 서버와 클라이언트의 연동, 그리고 웹 API의 설계 방법론 중 하나인 REST에 대해 알아보겠습니다.

## Topics

- expressJS, fastify
- AJAX, `XMLHttpRequest`, `fetch()`
- REST, CRUD
- CORS

## Resources

- [Express Framework](http://expressjs.com/)
- [Fastify Framework](https://www.fastify.io/)
- [MDN - Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [MDN - XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
- [REST API Tutorial](https://restfulapi.net/)
- [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)
- [MDN - CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

## Checklist

- 비동기 프로그래밍이란 무엇인가요?
  비동기 프로그래밍(Asynchronous programming)은 작업이 순차적으로 실행되는 동기적인 방식이 아닌, 작업이 완료되기 전에 다른 작업을 수행할 수 있도록 하여 시스템 자원의 효율성을 높이고 응답성을 높이는 프로그래밍 방식이다.
  동기적인 코드는 순서대로 실행되어 결과를 기다리며, 해당 코드의 실행이 완료되기 전까지 다른 작업을 수행하지 않는다. 이에 비해 비동기적인 코드는 비동기적인 함수를 사용하여 작업이 완료될 때까지 기다리지 않고 다른 작업을 수행하다가 작업이 완료되면 그 결과를 처리하는 방식이다.
  비동기 프로그래밍에서는 콜백(callback) 함수, 프로미스(promise), async/await 등의 방식을 사용하여 비동기 코드를 작성할 수 있다. 이러한 방식은 네트워크 요청, 파일 입출력, 데이터베이스 연동 등 시간이 오래 걸리는 작업을 비동기적으로 처리할 때 특히 유용하다.

  - 콜백을 통해 비동기적 작업을 할 때의 불편한 점은 무엇인가요? 콜백지옥이란 무엇인가요
    콜백을 통해 비동기적 작업을 처리할 때 가장 큰 불편함은 콜백 함수가 중첩될수록 코드의 복잡도가 증가하고 가독성이 떨어진다는 것이다. 이러한 현상을 "콜백 지옥"이라고 부르기도 한다.
    예를 들어, 파일을 읽어와서 파일 안에 포함된 URL을 가져오는 작업을 수행한다고 가정하면 이를 콜백 함수를 사용하여 처리하면 아래와 같이 코드가 중첩되어 가독성이 떨어지는 문제가 발생할 수 있다.

    fs.readFile('file.txt', 'utf8', function (err, data) {
    if (err) throw err;
    var urls = data.match(/https?:\/\/\S+/g);
    async.each(urls, function (url, callback) {
    request(url, function (error, response, body) {
    if (!error && response.statusCode == 200) {
    console.log(body);
    }
    callback();
    });
    }, function (err) {
    if (err) throw err;
    console.log('All urls have been fetched!');
    });
    });

    위 코드에서 fs.readFile() 함수로 파일을 읽어온 후, 파일 안에 포함된 URL을 가져오기 위해 data.match() 함수를 사용한다. 그리고 URL 리스트를 비동기적으로 하나씩 처리하기 위해 async.each() 함수를 호출하고, 각 URL을 가져오기 위해 request() 함수를 사용한다. 이러한 코드 구조에서는, 콜백 함수가 계속 중첩되면서 가독성이 떨어지는 콜백 지옥 현상이 발생할 수 있다.
    이러한 콜백 지옥을 해결하기 위해 등장한 것이 Promise나 async/await와 같은 비동기 처리 방식이다.

  - 자바스크립트의 Promise는 어떤 객체이고 어떤 일을 하나요?
    자바스크립트의 Promise는 비동기적 작업을 다룰 때 사용하는 객체다. Promise를 사용하면 비동기 작업을 좀 더 간편하게 처리할 수 있다.
    Promise는 기본적으로 비동기 작업이 완료될 때까지 기다렸다가 작업이 완료되면 결과를 반환한다. Promise를 생성할 때는 resolve와 reject 함수를 인자로 받는 함수를 만들어 전달한다. 이 함수는 비동기 작업을 수행하다가 성공하면 resolve 함수를 호출하고, 실패하면 reject 함수를 호출한다.
    Promise를 반환하는 함수를 호출할 때는 then과 catch 메서드를 사용하여 resolve와 reject 처리를 수행한다. then 메서드는 resolve 처리 결과를 받아 처리하고, catch 메서드는 reject 처리 결과를 받아 처리한다. 이를 통해 콜백 지옥을 피하고 가독성이 좋은 코드를 작성할 수 있다.

  - 자바스크립트의 `async`와 `await` 키워드는 어떤 역할을 하며 그 정체는 무엇일까요?
    async와 await 키워드는 ES2017(ES8)에서 추가된 기능으로, Promise를 기반으로 하는 비동기 코드를 동기적인 코드처럼 작성할 수 있도록 하는 문법이다.
    async 키워드는 함수를 선언할 때 사용하며, 해당 함수가 비동기 함수임을 나타낸다. 이를 통해 함수 내에서 await 키워드를 사용할 수 있게 된다.
    await 키워드는 Promise가 fulfilled 되었을 때 해당 값을 반환하며, Promise가 rejected 되었을 때는 예외를 발생시킨다. await는 Promise를 기다리는 동안 다른 코드가 실행되는 것을 막고, Promise가 반환하는 값을 변수에 할당하거나 다른 함수의 인수로 전달할 수 있게 해준다.
    async와 await을 사용하면, 콜백이나 Promise 체인을 사용하지 않고도 비동기적인 코드를 작성할 수 있다. 이를 통해 코드의 가독성을 높일 수 있고, 디버깅이나 유지보수가 쉬워진다.

- 브라우저 내 스크립트에서 외부 리소스를 가져오려면 어떻게 해야 할까요?
  브라우저 내 스크립트에서 외부 리소스를 가져오기 위해서는 XMLHttpRequest 객체나 fetch() API를 사용할 수 있다.
  XMLHttpRequest 객체를 사용하는 경우, 다음과 같이 작성할 수 있다.

  const xhr = new XMLHttpRequest();
  xhr.open('GET', '/data.json');
  xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
  console.log(xhr.responseText);
  }
  };
  xhr.send();

  fetch() API를 사용하는 경우, 다음과 같이 작성할 수 있다.

  fetch('/data.json')
  .then(response => response.json())
  .then(data => console.log(data));

  두 방법 모두 비동기적으로 리소스를 가져오며, fetch() API는 Promise를 반환하므로 then() 메소드를 사용하여 비동기적인 처리를 계속할 수 있다.

  - 브라우저의 `XMLHttpRequest` 객체는 무엇이고 어떻게 동작하나요?
    `XMLHttpRequest`는 브라우저에서 서버로 데이터를 비동기적으로 전송하거나 서버로부터 데이터를 비동기적으로 받아올 수 있는 기능을 제공하는 자바스크립트 객체이다.
    `XMLHttpRequest` 객체는 다음과 같은 방법으로 사용된다.

    1. `XMLHttpRequest` 객체를 생성
       const xhr = new XMLHttpRequest();
    2. `open()` 메서드를 사용하여 요청 메서드(GET, POST 등)와 요청 URL을 설정
       xhr.open('GET', '/api/data');
    3. `setRequestHeader()` 메서드를 사용하여 요청에 필요한 HTTP 헤더를 설정
       xhr.setRequestHeader('Content-Type', 'application/json');
    4. `onreadystatechange` 이벤트 핸들러를 등록하여 서버와의 통신 상태 변화를 감지
       xhr.onreadystatechange = function() {
       if (xhr.readyState === XMLHttpRequest.DONE && xhr.status === 200) {
       // 서버로부터 성공적으로 응답을 받았을 때 실행되는 코드
       }
       };
    5. `send()` 메서드를 호출하여 서버에 요청을 보냄
       xhr.send();

    위와 같이 `XMLHttpRequest` 객체를 사용하면 서버와 비동기적으로 데이터를 주고받을 수 있다. 요청을 보낸 후 서버로부터 응답이 도착하면 `onreadystatechange` 이벤트 핸들러가 호출되며, `readyState`와 `status` 프로퍼티를 통해 응답의 상태를 확인할 수 있다. 서버로부터 받은 데이터는 `responseText`나 `responseXML` 프로퍼티를 통해 가져올 수 있다.

  - `fetch` API는 무엇이고 어떻게 동작하나요?
    `fetch` API는 브라우저에서 제공하는 HTTP 요청을 보내는 기능을 제공하는 JavaScript API이다. `fetch` 함수를 호출하면 Promise 객체를 반환하며, 이 Promise 객체는 응답 데이터를 포함하는 `Response` 객체를 반환한다.
    `fetch` 함수는 두 개의 인수를 받는다. 첫 번째 인수는 요청을 보낼 URL이며, 두 번째 인수는 옵션 객체다. 옵션 객체는 HTTP 요청의 다양한 속성을 지정할 수 있는 속성들을 포함한다. 예를 들어 `method` 속성은 HTTP 요청 메소드를 지정하고, `headers` 속성은 HTTP 요청 헤더를 지정한다.
    `fetch` 함수는 HTTP 요청을 비동기적으로 보낸다. HTTP 요청이 완료되면 Promise 객체가 반환되며, 이 Promise 객체는 `Response` 객체를 포함한다. `Response` 객체는 응답 데이터를 포함하고, `headers` 속성을 통해 HTTP 응답 헤더 정보를 확인할 수 있다. 이후에는 `Response` 객체에서 `text()`, `json()`, `blob()`, `arrayBuffer()` 등의 메소드를 사용하여 응답 데이터를 처리할 수 있다.
    `fetch` API는 XHR(XMLHttpRequest) API와 달리 CORS (Cross-Origin Resource Sharing)를 적용하거나 다른 도메인의 API를 요청할 수 있어서 매우 유용하다. 또한, `fetch` API는 `async/await`와 함께 사용하면 더욱 직관적인 코드를 작성할 수 있다.

- REST는 무엇인가요?
  REST는 Representational State Transfer의 약자로, 웹 기반 시스템에서 서버와 클라이언트 간의 통신 방식을 정의한 아키텍처 스타일이다. REST는 HTTP 프로토콜을 기반으로 하며, 리소스(자원)를 정의하고, 리소스에 대한 주소(URI)를 사용하여 클라이언트가 서버에 요청을 보내고, 서버는 클라이언트에게 해당 리소스에 대한 상태 정보를 응답하는 방식으로 동작한다. REST는 아래와 같은 특징을 갖는다.

  클라이언트/서버 구조: 클라이언트와 서버가 각각 독립적으로 발전하고, 서로의 구현 내용을 알 필요가 없다.
  상태 없음(stateless): 클라이언트의 각 요청은 서버에 상태를 저장하지 않고, 단순히 해당 요청에 대한 응답만 제공한다.
  캐시 가능(cacheable): 클라이언트는 응답 결과를 캐시할 수 있어야 하며, 서버는 응답 결과에 캐시 가능 여부를 명시해야한다.
  계층 구조(layered system): 클라이언트는 직접 서버와 통신하지 않고, 중간 계층 서버를 통해 통신할 수 있다.
  인터페이스 일관성: REST API는 통일된 인터페이스를 사용하여 리소스를 조작하므로, 개발자가 쉽게 이해하고 사용할 수 있다.

  REST는 현재 대부분의 웹 API에서 사용되는 가장 일반적인 아키텍처 스타일 중 하나이다.

  - REST API는 어떤 목적을 달성하기 위해 나왔고 어떤 장점을 가지고 있나요?
    REST API는 Representational State Transfer의 약자로, 인터넷의 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처 스타일이다. REST API는 HTTP 기반으로 동작하며, 클라이언트와 서버 사이의 통신에서 상태를 관리하지 않고, 요청에 대한 응답만을 처리한다. REST API의 주요 목적은 웹의 기존 인프라를 활용하여 분산 하이퍼미디어 시스템을 구축하는 것이다. 이를 위해 REST API는 다음과 같은 특징을 가진다.

    자원(Resource)을 정의하고, 각 자원에 대한 주소를 지정
    HTTP Method를 사용하여 자원에 대한 CRUD(Create, Read, Update, Delete) 연산을 수행
    자원에 대한 표현(Representation)을 정의

    이러한 REST API의 특징을 통해 클라이언트와 서버 간의 분리와 상호 운용성을 향상시킬 수 있다. 또한, REST API를 사용하면 다양한 클라이언트와 서버 간의 호환성이 높아지고, 유지보수와 확장이 용이해진다.

  - RESTful한 API 설계의 단점은 무엇인가요?
    RESTful한 API 설계의 주요 단점은 다음과 같다.

    1. 복잡성: RESTful한 API 설계는 간단하고 직관적이지만, 대규모 애플리케이션에서는 복잡성이 증가할 수 있다. 이는 많은 엔드포인트, 매개변수 및 쿼리 매개변수, 다양한 HTTP 동사 등이 필요하기 때문이다.
    2. 성능: RESTful한 API는 대부분 HTTP 프로토콜을 기반으로 하며, HTTP 연결을 맺고 끊는 데 시간이 걸린다. 또한 요청과 응답의 크기가 클 경우에는 처리 시간이 더 걸릴 수 있다.
    3. 보안: RESTful한 API 설계는 기본적으로 인증 및 권한 부여 기능을 제공하지 않는다. 이를 위해서는 추가적인 보안 체계가 필요하며, 이로 인해 복잡성이 증가할 수 있다.
    4. 캐싱: RESTful한 API는 캐싱 기능을 지원하지만, 캐싱 전략이 잘못 구현될 경우 오래된 데이터가 클라이언트에게 전달될 수 있다.
    5. 버전 관리: RESTful한 API 설계에서는 버전 관리가 필요하다. 새로운 엔드포인트가 추가되거나 기존 엔드포인트가 변경되는 경우 API 버전을 관리하여 호환성을 유지해야한다. 이는 개발자의 작업량과 API 사용자의 혼란을 야기할 수 있다.

- CORS란 무엇인가요? 이러한 기능이 왜 필요할까요? CORS는 어떻게 구현될까요?
  CORS는 Cross-Origin Resource Sharing의 약자로, 웹 애플리케이션에서 다른 출처(origin)의 리소스에 접근할 때 발생하는 보안 상의 문제를 해결하기 위한 메커니즘이다.
  브라우저에서 웹 페이지를 로드할 때, 해당 페이지가 위치한 도메인(origin)에서 리소스를 요청하는 것은 보안 상 안전하다. 하지만 웹 애플리케이션이 다른 도메인의 리소스를 요청할 경우, 보안 문제가 발생할 수 있다. 이때 CORS를 사용하여 다른 출처의 리소스에 접근할 수 있도록 허용하도록 구성할 수 있다.
  CORS는 브라우저에서 구현되며, HTTP 헤더를 통해 동작한다. 클라이언트는 HTTP 요청을 보낼 때, 요청 헤더 중 `Origin` 헤더에 자신의 도메인 정보를 담아서 보낸다. 서버는 이 `Origin` 정보를 확인하고, 해당 도메인이 리소스에 접근할 수 있는지 여부를 판단한다. 서버가 해당 도메인의 접근을 허용할 경우, 응답 헤더에 `Access-Control-Allow-Origin` 헤더를 추가하여 응답을 클라이언트에게 반환한다. 이후 클라이언트는 이 응답을 받아서 리소스를 사용할 수 있다.
  CORS는 보안 상의 이유로 기본적으로 다른 도메인에 대한 접근을 허용하지 않는다. 그러나 웹 애플리케이션에서 다른 출처의 리소스를 필요로 하는 경우, CORS를 통해 다른 도메인에 대한 접근을 허용할 수 있다.

## Quest

- 이번 퀘스트는 Midterm에 해당하는 과제입니다. 분량이 제법 많으니 한 번 기능별로 세부 일정을 정해 보고, 과제 완수 후에 그 일정이 얼마나 지켜졌는지 스스로 한 번 돌아보세요.
  - 이번 퀘스트부터는 skeleton을 제공하지 않습니다!
- Quest 05에서 만든 메모장 시스템을 서버와 연동하는 어플리케이션으로 만들어 보겠습니다.
  - 클라이언트는 `fetch` API를 통해 서버와 통신합니다.
  - 서버는 8000번 포트에 REST API를 엔드포인트로 제공하여, 클라이언트의 요청에 응답합니다.
  - 클라이언트로부터 온 새 파일 저장, 삭제, 다른 이름으로 저장 등의 요청을 받아 서버의 로컬 파일시스템을 통해 저장되어야 합니다.
    - 서버에 어떤 식으로 저장하는 것이 좋을까요?
  - API 서버 외에, 클라이언트를 띄우기 위한 서버가 3000번 포트로 따로 떠서 API 서버와 서로 통신할 수 있어야 합니다.
  - Express나 Fastify 등의 프레임워크를 사용해도 무방합니다.
- 클라이언트 프로젝트와 서버 프로젝트 모두 `npm i`만으로 디펜던시를 설치하고 바로 실행될 수 있게 제출되어야 합니다.
- 이번 퀘스트부터는 앞의 퀘스트의 결과물에 의존적인 경우가 많습니다. 제출 폴더를 직접 만들어 제출해 보세요!

## Advanced

- `fetch` API는 구현할 수 없지만 `XMLHttpRequest`로는 구현할 수 있는 기능이 있을까요?
- REST 이전에는 HTTP API에 어떤 패러다임들이 있었을까요? REST의 대안으로는 어떤 것들이 제시되고 있을까요?
