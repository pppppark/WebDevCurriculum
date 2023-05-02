# Quest 13. 웹 API의 응용과 GraphQL

## Introduction

- 이번 퀘스트에서는 차세대 웹 API의 대세로 각광받고 있는 GraphQL에 대해 알아보겠습니다.

## Topics

- GraphQL
  - Schema
  - Resolver
  - DataLoader
- Apollo

## Resources

- [GraphQL](https://graphql.org/)
- [GraphQL.js](http://graphql.org/graphql-js/)
- [DataLoader](https://github.com/facebook/dataloader)
- [Apollo](https://www.apollographql.com/)

## Checklist

- GraphQL API는 무엇인가요? REST의 어떤 단점을 보완해 주나요?
  GraphQL API는 클라이언트에서 요청한 데이터만 서버에서 응답으로 보내주는 쿼리 언어다. REST API와는 달리 클라이언트가 필요한 데이터를 정확하게 요청할 수 있고, 서버에서는 해당 요청에 대해서만 필요한 데이터를 응답으로 보내주는 특징이 있다.
  REST API에서는 클라이언트에서 요청한 데이터의 구조와 서버에서 응답으로 보내줄 데이터의 구조가 미리 정해져 있어야한다. 따라서, 클라이언트에서 필요한 데이터를 가져오기 위해 여러 개의 API를 호출해야 할 때도 있다. 또한, API 버전 업그레이드 시에 클라이언트와 서버 사이의 호환성을 맞추기 위해 많은 노력이 필요한다.
  반면에 GraphQL API는 클라이언트에서 필요한 데이터의 구조를 클라이언트가 직접 정의하고 요청할 수 있다. 이를 통해 클라이언트는 필요한 데이터를 하나의 요청으로 가져올 수 있다. 또한, 서버 측에서도 필요한 데이터를 하나의 응답으로 보내주기 때문에, REST API와 달리 여러 번의 API 호출이 필요하지 않다. API 버전 업그레이드 시에도 클라이언트와 서버 사이의 호환성을 맞추는 것이 쉽다. 이러한 이점들로 인해, GraphQL API는 REST API의 단점을 보완해준다.

- GraphQL 스키마는 어떤 역할을 하며 어떤 식으로 정의되나요?
  GraphQL 스키마는 GraphQL API에서 제공되는 데이터의 구조와 타입에 대한 정의를 담고 있는 핵심적인 구성 요소이다. 스키마를 통해 GraphQL API를 구성하고 사용하는 클라이언트가 요청할 수 있는 쿼리와 데이터의 구조, 타입을 미리 정의하고 문서화할 수 있다.
  스키마는 타입 정의와 리졸버 함수로 구성된다. 타입은 스칼라 타입(문자열, 숫자, 불리언 등)과 객체 타입, 인터페이스 타입, 열거형 타입 등이 있으며, 이를 통해 데이터의 구조를 정의한다. 리졸버 함수는 각각의 필드에 대한 데이터를 가져오는 로직을 구현하는 함수로, 클라이언트에서 요청한 쿼리에 해당하는 데이터를 반환한다.
  스키마는 일반적으로 SDL(Schema Definition Language) 형식으로 작성되며, 이는 간단한 문법으로 스키마를 정의할 수 있도록 해준다. 스키마를 작성하고 빌드한 후에는 API의 모든 요청에 대해 적절한 응답을 제공할 수 있게 된다.

- GraphQL 리졸버는 어떤 역할을 하며 어떤 식으로 정의되나요?
  GraphQL 리졸버(resolver)는 GraphQL 스키마에 정의된 쿼리, 뮤테이션, 서브스크립션과 같은 필드를 해결하는 함수이다. 각각의 필드는 데이터 소스에서 가져온 데이터를 나타내며, 리졸버는 이러한 데이터를 반환하는 역할을 한다.

  fieldName: (obj, args, context, info) => result;

  - fieldName: 리졸버가 해결할 필드 이름
  - obj: 부모 객체로부터 상속된 객체
    일반적으로 사용되는 경우는 특정 데이터베이스에서 쿼리 정보
  - args: 쿼리에서 전달된 인자
    필드가 인수를 허용하는 경우 사용
  - context: 모든 리졸버에서 공유하는 객체
    일반적으로 인증 정보나 데이터베이스 연결과 같은 것이 포함
  - info: 현재 쿼리 실행에 대한 정보
    일반적으로 스키마 정보나 리졸버 경로를 포함
  - result: 해당 필드에서 반환되는 값

  리졸버는 필요한 데이터를 가져오기 위해 데이터베이스, REST API, 캐시 등의 데이터 소스와 상호 작용한다. 리졸버는 비동기 함수로 작성될 수 있으며, 여러 리졸버에서 공유되는 컨텍스트 객체에 대한 참조를 받아 작업을 수행한다.
  GraphQL에서 리졸버는 스키마를 정의하는 데 중요한 역할을 한다. 스키마에 정의된 필드에 대해 쿼리를 실행하면, 해당 필드에 대해 리졸버 함수가 실행되어 결과 값을 반환한다. 따라서 리졸버를 올바르게 구현하는 것은 GraphQL API의 정확성과 성능을 보장하는 데 매우 중요하다.

  - GraphQL 리졸버의 성능 향상을 위한 DataLoader는 무엇이고 어떻게 쓰나요?
    DataLoader는 GraphQL에서 쿼리가 복수의 데이터를 가져와야 할 때, 데이터베이스나 외부 API와 같은 데이터 소스로부터 데이터를 효율적으로 가져오기 위한 라이브러리다. DataLoader는 쿼리를 수행하기 전에 중복 요청을 제거하고, 데이터 소스에서 한 번에 여러 데이터를 가져와서 요청 시간과 데이터베이스 부하를 줄이는 등의 효율적인 처리를 가능하게 한다.
    DataLoader를 사용하기 위해서는 일단 DataLoader 패키지를 설치해야 한다. 그리고 각 필드에 대한 DataLoader를 생성하고, 각 필드 리졸버에서 해당 DataLoader를 사용하여 데이터를 가져온다. 예를 들어, User와 Post 모델이 있고, User에서 Post를 가져오는 필드가 있다면, 이 필드의 DataLoader를 다음과 같이 정의할 수 있다.

    const postLoader = new DataLoader(async (userIds) => {
    const posts = await Post.find({ userId: { $in: userIds } });
    const postsByUser = \_.groupBy(posts, 'userId');
    return userIds.map((id) => postsByUser[id] || []);
    });

    const userType = new GraphQLObjectType({
    name: 'User',
    fields: () => ({
    id: { type: GraphQLID },
    name: { type: GraphQLString },
    posts: {
    type: new GraphQLList(postType),
    resolve: (user, args, context) => {
    return context.postLoader.load(user.id);
    },
    },
    }),
    });

위 코드에서 postLoader는 userIds 배열을 받아 각 사용자의 포스트 목록을 반환하는 DataLoader다. postType은 포스트에 대한 GraphQLObjectType다. 그리고 User 타입의 posts 필드에서 context.postLoader.load(user.id)를 호출하여 해당 사용자의 포스트를 가져온다. DataLoader는 이를 받아 중복 요청을 제거하고, 한 번에 여러 데이터를 가져와서 데이터 소스의 부하를 줄여서 성능 향상을 이루게 된다.

이렇게 DataLoader를 사용하면 N+1 쿼리 문제를 해결하고, 복수의 데이터 소스로부터 데이터를 가져올 때도 효율적으로 처리할 수 있다.

- 클라이언트 상에서 GraphQL 요청을 보내려면 어떻게 해야 할까요?
  클라이언트 상에서 GraphQL 요청을 보내기 위해서는 보통 다음과 같은 방법들을 사용한다.

  1. HTTP Request
     GraphQL은 HTTP(S) 프로토콜을 사용하는 REST API와 마찬가지로 HTTP Request를 통해 요청한다. HTTP POST 요청을 보내고, 요청 본문(Request Body)에 GraphQL 쿼리를 포함시킨다.
  2. GraphQL 클라이언트 라이브러리
     GraphQL 클라이언트 라이브러리를 사용하면, 별도의 HTTP 요청 코드를 작성하지 않고도 쉽게 GraphQL API를 호출할 수 있다. 대표적인 GraphQL 클라이언트 라이브러리로는 Apollo Client, Relay 등이 있다.
  3. GraphiQL, Playground
     GraphiQL과 Playground는 GraphQL API를 쉽게 테스트하고, 쿼리를 작성하고 실행할 수 있는 웹 기반의 개발도구이다. 쿼리와 변수를 입력하면, API 응답과 함께 결과를 시각화하여 보여준다.
  4. cURL
     cURL은 명령줄 기반의 데이터 전송 도구다. HTTP 요청을 보내는 데 사용할 수 있으며, 이를 통해 GraphQL API를 호출할 수 있다.

  위 방법들 중 적절한 방법을 선택하여 클라이언트 상에서 GraphQL 요청을 보내면 된다.

  - Apollo 프레임워크(서버/클라이언트)의 장점은 무엇일까요?
    Apollo는 GraphQL 서버와 클라이언트를 개발하기 위한 프레임워크

    1. 쉬운 개발 경험: Apollo는 개발자가 쉽게 GraphQL API를 작성하고 사용할 수 있도록 설계되어 있다. Apollo Server는 GraphQL API를 쉽게 작성하고 실행할 수 있도록 지원하며, Apollo Client는 GraphQL API에 대한 데이터를 쉽게 가져올 수 있도록 지원한다.
    2. 성능 최적화: Apollo는 데이터 요청과 응답을 최적화하여 네트워크 대역폭과 데이터 전송 속도를 향상시킨다. Apollo Client는 데이터 요청과 응답을 캐시하고 미리 가져오기 기능을 지원한다.
    3. 유연성: Apollo는 다양한 백엔드 서비스와 통합할 수 있다. Apollo Server는 다양한 데이터 소스와 통합할 수 있으며, Apollo Client는 다양한 데이터 저장소와 통합할 수 있다.
    4. 강력한 개발 도구: Apollo는 개발자가 GraphQL API를 작성하고 디버깅하는 데 필요한 다양한 도구를 제공한다. 예를 들어, Apollo Server는 GraphQL Playground라는 웹 기반 IDE를 제공하여 개발자가 API를 테스트하고 디버깅할 수 있다.
    5. 커뮤니티: Apollo는 커뮤니티 기반으로 운영되며, 커뮤니티에서는 다양한 문제에 대한 해결책을 제시하고 지원한다. 또한, Apollo는 다양한 문서와 튜토리얼을 제공하여 개발자가 쉽게 시작할 수 있도록 돕는다.

  - Apollo Client를 쓰지 않고 Vanilla JavaScript로 GraphQL 요청을 보내려면 어떻게 해야 할까요?
    Vanilla JavaScript로 GraphQL 요청을 보내기 위해서는 `fetch()` 함수나 `XMLHttpRequest` 객체를 사용하여 HTTP POST 요청을 보내고, `body`에 GraphQL 쿼리를 포함시켜야 한다. 다음과 같이 `fetch()` 함수를 사용하여 GraphQL 요청을 보낼 수 있다.

        fetch('/graphql', {
        method: 'POST',
        headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
        },
        body: JSON.stringify({
        query: `     query {

    posts {
    id
    title
    content
    }
    }`
    })
    })
    .then(response => response.json())
    .then(data => console.log(data));

        위 코드에서는 `fetch()` 함수를 호출할 때 두 개의 인자를 전달한다. 첫 번째 인자는 요청을 보낼 URL(`/graphql`)을 지정하고, 두 번째 인자는 HTTP 요청에 필요한 옵션을 포함하는 객체다. 두 번째 인자에서는 요청의 메서드(`method`), 요청의 헤더(`headers`), 그리고 요청의 본문(`body`)을 설정한다.

        GraphQL 요청의 본문은 JSON 형식으로 지정합니다. `query` 필드에는 실행할 GraphQL 쿼리를 지정하고, `variables` 필드에는 쿼리에 전달할 변수를 지정할 수 있다. 위 코드에서는 `variables` 필드를 사용하지 않았으므로 생략했다.

        요청에 대한 응답이 오면, `response.json()` 메서드를 호출하여 JSON 형식으로 응답을 파싱한다. 파싱된 데이터는 `data` 변수에 저장됩니다. 이후에는 `data` 변수를 적절하게 처리하면 된다.

- GraphQL 기반의 API를 만들 때 에러처리와 HTTP 상태코드 등은 어떻게 하는게 좋을까요?
  GraphQL 기반의 API를 만들 때 에러처리와 HTTP 상태코드를 다루는 것은 중요하다. 이를 통해 클라이언트에서 API를 사용하는 동안 발생하는 오류를 이해하고 해결할 수 있다.

  GraphQL API에서는 일반적으로 다음과 같은 HTTP 상태코드를 사용한다.

  - 200 OK: 성공적인 요청에 대한 응답
  - 400 Bad Request: 클라이언트가 잘못된 요청을 보낸 경우
  - 401 Unauthorized: 인증되지 않은 요청일 경우
  - 403 Forbidden: 요청에 대한 권한이 없는 경우
  - 404 Not Found: 요청한 자원이 없는 경우
  - 500 Internal Server Error: 서버에서 오류가 발생한 경우

  또한 GraphQL API에서는 다음과 같은 예외 처리 방법을 사용할 수 있다.

  - Resolver에서 예외를 throw하여 GraphQL 쿼리/뮤테이션 실행 중 예외를 처리할 수 있다.
  - GraphQL 스키마에서는 field resolver에서 throw한 예외를 핸들링 할 수 있는 `@catch` 데코레이터를 제공한다.
  - 전역적으로 예외를 처리할 수 있는 미들웨어를 등록하여 예외를 처리할 수 있다.

  에러 메시지를 클라이언트로 전송할 때는 보안상의 이유로 디버그 정보를 포함하지 않도록 주의해야한다. 디버그 정보를 포함하면 악의적인 사용자가 그 정보를 이용하여 공격할 수 있다. 따라서 GraphQL API에서는 에러 메시지를 표준화하고, 안전하게 전송하는 방법을 사용하는 것이 좋다. 예를 들어, GraphQL 스펙에서는 `errors` 필드를 통해 여러 개의 에러를 JSON으로 반환하도록 규정하고 있다.

## Quest

- 메모장의 서버와 클라이언트 부분을 GraphQL API로 수정해 보세요.

## Advanced

- GraphQL이 아직 제대로 수행하지 못하거나 불가능한 요구사항에는 어떤 것이 있을까요?
- GraphQL의 경쟁자에는 어떤 것이 있을까요?
