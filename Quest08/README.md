# Quest 08. 웹 API의 기초

## Introduction

- 이번 퀘스트에서는 웹 API 서버의 기초를 알아보겠습니다.

## Topics

- HTTP Method
- node.js `http` module
  - `req`와 `res` 객체

## Resources

- [MDN - Content-Type Header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type)
- [MDN - HTTP Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [MDN - MIME Type](https://developer.mozilla.org/en-US/docs/Glossary/MIME_type)
- [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)
- [HTTP Node.js Manual & Documentation](https://nodejs.org/api/http.html)

## Checklist

- HTTP의 GET과 POST 메소드는 어떻게 다른가요?
  HTTP의 GET과 POST 메소드는 HTTP 요청에서 사용되는 두 가지 주요 메소드이다. 이 두 메소드는 서로 목적이 다르며, 다음과 같은 차이점이 있다.

  GET 메소드: 데이터를 서버로부터 가져올 때 사용된다. URL에 데이터를 포함시켜 요청을 보내며, 요청한 데이터가 URL에 노출된다. 따라서 데이터가 노출되기 때문에 보안에 취약하다. 또한 요청한 데이터가 URL에 포함되기 때문에 길이에 제한이 있다.
  POST 메소드: 서버에 데이터를 전송할 때 사용된다. 요청 본문에 데이터를 포함시켜 요청을 보내며, URL에 데이터가 노출되지 않는다. 따라서 GET 메소드보다 보안성이 높다. 또한 요청한 데이터가 URL에 포함되지 않기 때문에 길이의 제한이 없다.

  이러한 차이로 인해 GET 메소드는 데이터를 가져오는 데 사용되고, POST 메소드는 데이터를 서버로 보내는 데 사용된다. 그러나 이외에도 HTTP 메소드에는 다양한 종류가 있으며, 각각의 목적과 특징이 있다.

  - 다른 HTTP 메소드에는 무엇이 있나요?
    GET과 POST 메소드를 제외한 다른 메소드들은 다음과 같다.

    PUT: 클라이언트에서 서버로 데이터를 전송한다. 주로 리소스를 업데이트할 때 사용한다.
    DELETE: 클라이언트에서 서버로 리소스 삭제 요청을 전송한다.
    HEAD: GET과 유사하지만, 응답 본문을 제외한 응답 헤더만을 받는다.
    CONNECT: 클라이언트와 서버 간의 터널링 프로토콜을 설정한다.
    OPTIONS: 서버가 지원하는 메소드 목록을 요청한다.
    TRACE: 클라이언트에서 서버로 요청 메시지를 보내고, 서버에서는 해당 요청을 그대로 되돌려주는 메소드로, 디버깅 용도로 사용된다.
    PATCH: 리소스의 일부를 수정할 때 사용한다.

    이외에도 PROPFIND, MKCOL, COPY, MOVE 등의 메소드도 있지만, 이들은 주로 WebDAV와 같은 확장된 웹 프로토콜에서 사용된다.

- HTTP 서버에 GET과 POST를 통해 데이터를 보내려면 어떻게 해야 하나요?
  HTTP 서버에 GET 메소드를 통해 데이터를 보내려면 URL의 쿼리 파라미터를 이용하여 데이터를 전송한다. 쿼리 파라미터는 URL 끝에 ?를 붙이고 파라미터 이름과 값 쌍을 &로 구분하여 나열한 것이다. 예를 들어, http://example.com/search?q=apple&category=fruit와 같은 URL은 q=apple과 category=fruit라는 두 개의 쿼리 파라미터를 가지고 있다.
  POST 메소드를 통해 데이터를 보내려면 HTTP 요청 본문에 데이터를 포함시킨다. 이 때 데이터는 일반적으로 URL-encoded나 JSON 형태로 전송된다. URL-encoded 방식은 데이터를 key=value 쌍으로 만든 후, &로 구분하여 전송한다. 예를 들어, name=john&age=30과 같은 데이터를 전송할 수 있다. JSON 방식은 데이터를 JSON 형태로 만든 후, HTTP 요청 본문에 포함시킨다.
  HTTP 클라이언트는 데이터를 보내기 위해 알맞은 메소드와 함께 요청을 보내면 된다. 이 때, GET 메소드는 데이터를 요청하는 용도로 사용하고, POST 메소드는 데이터를 생성하거나 업데이트하는 용도로 사용한다.

  - HTTP 요청의 `Content-Type` 헤더는 무엇인가요?
    HTTP 요청의 Content-Type 헤더는 해당 요청이 전송하는 데이터의 유형을 나타내는 미디어 타입을 지정한다. 미디어 타입은 일반적으로 MIME 타입 형식으로 지정된다.
    예를 들어, Content-Type: application/json 헤더는 해당 요청이 JSON 데이터를 전송한다는 것을 나타내며, Content-Type: text/html 헤더는 해당 요청이 HTML 문서를 전송한다는 것을 나타낸다.
    HTTP 요청의 Content-Type 헤더는 서버가 요청의 본문(body)을 올바르게 해석하고 처리할 수 있도록 도와준다. 서버가 이 헤더를 제대로 이해하지 못하면 요청을 처리할 수 없거나 잘못 처리할 가능성이 있다.

  - Postman에서 POST 요청을 보내는 여러 가지 방법(`form-data`, `x-www-form-urlencoded`, `raw`, `binary`) 각각은 어떤 용도를 가지고 있나요?
    Postman에서 POST 요청을 보내는 방법으로는 form-data, x-www-form-urlencoded, raw, binary 등이 있다. 각각의 방법은 다음과 같은 용도를 가지고 있다.

    1. form-data: 파일 업로드를 위한 방식으로, 폼 데이터를 multipart/form-data 형식으로 보낸다. 파일 데이터나 바이너리 데이터를 보낼 수 있다.
    2. x-www-form-urlencoded: 폼 데이터를 URL-encoded 형식으로 보내는 방식이다. 보통 폼 데이터를 전송할 때 사용한다. key-value 형태로 데이터를 전송할 수 있습니다.
    3. raw: JSON, XML 등의 데이터를 직접 입력해 전송하는 방식입니다. 보통 API를 호출할 때 사용힌다.
    4. binary: 바이너리 데이터를 보내는 방식이다. 이미지나 오디오, 비디오 등의 데이터를 보낼 때 사용한다.

    각각의 방식은 서로 다른 형식으로 데이터를 전송하기 때문에, 사용하려는 데이터의 형식에 맞게 선택해야 한다. 예를 들어, 파일을 업로드할 때는 form-data 방식을 사용하고, JSON 데이터를 전송할 때는 raw 방식을 사용한다.

- node.js의 `http` 모듈을 통해 HTTP 요청을 처리할 때,

  - `req`와 `res` 객체에는 어떤 정보가 담겨있을까요?
    http 모듈을 사용하여 서버를 만들 경우, 클라이언트로부터 요청이 들어오면 콜백 함수에 전달되는 req(HTTP 요청) 객체와, 응답을 보내기 위한 res(HTTP 응답) 객체를 사용한다. 각 객체에는 다음과 같은 정보들이 담겨있다.

    req.method: HTTP 요청 메서드 (GET, POST, PUT 등)
    req.url: 클라이언트가 요청한 URL
    req.headers: HTTP 요청 헤더 (객체 형태)
    req.params: URL의 파라미터 (라우팅에서 사용)
    req.query: URL의 쿼리스트링 (객체 형태)
    req.body: HTTP 요청 바디 (POST 등의 경우)
    res.statusCode: HTTP 응답 코드 (200, 404, 500 등)
    res.setHeader(name, value): HTTP 응답 헤더를 설정
    res.write(chunk): HTTP 응답 바디의 일부분을 보냄
    res.end([data]): HTTP 응답 바디를 보내고 응답을 종료

    req와 res 객체는 HTTP 프로토콜의 요청과 응답을 추상화한 객체로, 이를 통해 서버와 클라이언트 간의 통신을 처리할 수 있다. 이외에도 http 모듈은 다양한 메서드를 제공하며, 이를 활용하여 원하는 서버를 만들 수 있다.

  - GET과 POST에 대한 처리 형태가 달라지는 이유는 무엇인가요?
    node.js의 http 모듈을 통해 HTTP 요청을 처리할 때, GET과 POST에 대한 처리 형태가 달라지는 이유는 HTTP 요청 메시지의 형태와 의미가 다르기 때문이다.
    GET 요청은 주로 서버로부터 리소스를 가져오는데 사용되며, URL의 쿼리스트링에 데이터를 전송한다. 따라서 GET 요청은 http.IncomingMessage 객체의 url 속성을 통해 URL을 파싱하고, querystring 모듈을 사용하여 쿼리스트링에 포함된 데이터를 추출할 수 있다.
    반면에 POST 요청은 주로 서버에 데이터를 전송하는데 사용되며, HTTP 요청 메시지의 본문에 데이터를 담아 전송한다. 따라서 POST 요청은 http.IncomingMessage 객체의 data 이벤트와 end 이벤트를 통해 HTTP 요청 메시지의 본문 데이터를 추출하고, querystring 모듈이나 body-parser와 같은 미들웨어를 사용하여 본문 데이터를 파싱할 수 있다.
    GET 요청과 POST 요청은 HTTP 요청 메시지의 형태와 의미가 다르기 때문에 서버에서의 처리 방식도 달라지게 된다.

- 만약 API 엔드포인트(URL)가 아주 많다고 한다면, HTTP POST 요청의 `Content-Type` 헤더에 따라 다른 방식으로 동작하는 서버를 어떻게 정리하면 좋을까요?
  API 엔드포인트가 많다면 Content-Type 헤더에 따라 다른 방식으로 동작하는 서버를 관리하기가 어려울 수 있다. 이 경우, 다음과 같은 방법을 고려해 볼 수 있다.

  1. 중개 프로그램 사용: API 요청을 받는 중개 프로그램을 만들어서 Content-Type 헤더에 따라 요청을 처리하는 서버로 라우팅한다. 예를 들어, application/json인 경우 JSON 요청을 처리하는 서버로 라우팅하고, application/x-www-form-urlencoded인 경우 폼 데이터를 처리하는 서버로 라우팅한다.
  2. 컨트롤러 분리: 컨트롤러를 Content-Type 헤더에 따라 분리하여 서로 다른 컨트롤러로 분리한다. 예를 들어, JSON 요청을 처리하는 컨트롤러와 폼 데이터를 처리하는 컨트롤러를 분리한다. 이렇게 분리하면 코드의 가독성과 유지보수성이 향상된다.
  3. 미들웨어 사용: 미들웨어를 사용하여 Content-Type 헤더에 따라 요청을 처리한다. 미들웨어는 요청이 처리되기 전에 실행되는 함수로, 요청을 가공하거나 검증하는 역할을 한다. 예를 들어, body-parser 모듈을 사용하여 application/json 및 application/x-www-form-urlencoded 요청을 처리하는 미들웨어를 만들 수 있다.
  4. 프레임워크 사용: Express, Koa, Hapi와 같은 Node.js 웹 프레임워크를 사용하면 Content-Type 헤더에 따라 다른 방식으로 동작하는 API를 쉽게 관리할 수 있다. 이러한 프레임워크는 미들웨어를 사용하여 요청을 처리하며, 라우팅과 컨트롤러를 간편하게 정의할 수 있다.

  - 그 밖에 서버가 요청들에 따라 공통적으로 처리하는 일에는 무엇이 있을까요? 이를 어떻게 정리하면 좋을까요?
    API 엔드포인트가 많다면, 엔드포인트의 처리 로직을 각각의 파일이나 모듈로 분리하여 관리하는 것이 좋다. 예를 들어, GET /users와 POST /users의 처리 로직을 각각 별도의 파일로 분리하여 관리할 수 있다.
    HTTP POST 요청의 Content-Type 헤더에 따라 다른 방식으로 동작하는 서버를 관리하기 위해서는, 해당 Content-Type에 따른 엔드포인트 처리 로직을 분리하여 별도의 파일이나 모듈로 만들어서 관리하는 것이 좋다. 예를 들어, application/json과 application/x-www-form-urlencoded 형식으로 전송되는 데이터를 처리하는 엔드포인트 처리 로직을 각각의 파일로 분리하여 관리할 수 있다.
    서버가 요청들에 따라 공통적으로 처리하는 일로는 로깅, 인증, 보안 등이 있습니다. 이러한 공통적인 처리 로직은 미들웨어로 구현하여 각 엔드포인트 처리 로직에서 재사용할 수 있다. 미들웨어는 요청 처리 전에 실행되며, 요청 처리 후에도 추가적인 처리를 할 수 있다. 예를 들어, 요청이 들어올 때 로그를 남기는 로깅 미들웨어나 요청에 대한 인증을 처리하는 인증 미들웨어 등을 만들어서 사용할 수 있다. 또한, 미들웨어를 사용하여 CORS 처리, JSON 파싱 등과 같이 HTTP 요청/응답과 관련된 일반적인 처리 로직을 관리할 수 있다.
    서버의 코드를 정리하기 위해서는 역할별로 모듈이나 파일을 분리하는 것이 좋다. 예를 들어, 엔드포인트 처리 로직과 미들웨어를 분리하여 관리하거나, 데이터베이스와의 연동을 위한 모듈을 별도로 만들어서 사용할 수 있다. 이를 통해 코드의 가독성과 유지보수성을 높일 수 있다.

## Quest

- 다음의 동작을 하는 서버를 만들어 보세요.
  - 브라우저의 주소창에 `http://localhost:8080`을 치면 `Hello World!`를 응답하여 브라우저에 출력합니다.
  - 서버의 `/foo` URL에 `bar` 변수로 임의의 문자열을 GET 메소드로 보내면, `Hello, [문자열]`을 출력합니다.
  - 서버의 `/foo` URL에 `bar` 키에 임의의 문자열 값을 갖는 JSON 객체를 POST 메소드로 보내면, `Hello, [문자열]`을 출력합니다.
  - 서버의 `/pic/upload` URL에 그림 파일을 POST 하면 서버에 보안상 적절한 방법으로 파일이 업로드 됩니다.
  - 서버의 `/pic/show` URL을 GET 하면 브라우저에 위에 업로드한 그림이 뜹니다.
  - 서버의 `/pic/download` URL을 GET 하면 브라우저에 위에 업로드한 그림이 `pic.jpg`라는 이름으로 다운로드 됩니다.
- expressJS와 같은 외부 프레임워크를 사용하지 않고, node.js의 기본 모듈만을 사용해서 만들어 보세요.
- 처리하는 요청의 종류에 따라 공통적으로 나타나는 코드를 정리해 보세요.

## Advanced

- 서버가 파일 업로드를 지원할 때 보안상 주의할 점에는 무엇이 있을까요?
