# Quest 03. 자바스크립트와 DOM

## Introduction

- 자바스크립트는 현재 웹 생태계의 근간인 프로그래밍 언어입니다. 이번 퀘스트에서는 자바스크립트의 기본적인 문법과, 자바스크립트를 통해 브라우저의 실제 DOM 노드를 조작하는 법에 대하여 알아볼 예정입니다.

## Topics

- 자바스크립트의 역사
- 기본 자바스크립트 문법
- DOM API
  - `document` 객체
  - `document.getElementById()`, `document.querySelector()`, `document.querySelectorAll()` 함수들
  - 기타 DOM 조작을 위한 함수와 속성들
- 변수의 스코프
  - `var`, `let`, `const`

## Resources

- [자바스크립트 첫걸음](https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps)
- [자바스크립트 구성요소](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Building_blocks)
- [Just JavaScript](https://justjavascript.com/)

## Checklist

- 자바스크립트는 버전별로 어떻게 변화하고 발전해 왔을까요?
  JavaScript 1.0 (1995) - 초기 버전으로, 변수, 연산자, 함수, 객체 등을 포함하고 있다.
  JavaScript 1.1 (1996) - 예외 처리 및 정규 표현식 기능이 추가되었다.
  JavaScript 1.2 (1998) - CSS 스타일 속성을 제어할 수 있는 DOM(Document Object Model) 기능과 iframe 등이 추가되었다.
  JavaScript 1.3 (1998) - XML 데이터를 처리하는 기능과 정렬, 검색 등의 배열 기능이 개선되었다.
  JavaScript 1.4 (1999) - 더욱 발전된 배열 메서드와 강력한 정규 표현식 기능이 추가되었다.
  ECMAScript 3 (1999) - ECMA 규격에 따라 정식 스펙이 발표되었으며, try-catch문, switch문 등의 기능이 추가되었다.
  ECMAScript 4 (취소됨) - 새로운 객체 모델 및 클래스 기능, 람다 함수, 제네릭 등의 기능이 추가될 예정이었지만, 스펙화 작업이 중단되어 버린 버전이다.
  ECMAScript 5 (2009) - strict 모드, JSON 객체, Object.keys() 등의 기능이 추가되었다.
  ECMAScript 6 (2015) - 대규모 업그레이드로, 화살표 함수, 클래스, 템플릿 리터럴, for...of 반복문 등의 기능이 추가되었다.
  ECMAScript 7 (2016) - Array.prototype.includes() 메서드와 지수 연산자(\*\*) 등의 기능이 추가되었다.
  ECMAScript 8 (2017) - async/await 함수, Object.entries()와 Object.values() 메서드 등의 기능이 추가되었다.
  ECMAScript 9 (2018) - rest/spread 프로퍼티, Promise.finally() 메서드 등의 기능이 추가되었다.
  ECMAScript 10 (2019) - Array.prototype.flat() 메서드와 String.prototype.trimStart() 등의 기능이 추가되었다.
  ECMAScript 2019 (ES10.1) (2020) - String.prototype.matchAll() 메서드와 globalThis 객체 등의 기능이 추가되었다.

  - 자바스크립트의 버전들을 가리키는 ES5, ES6, ES2016, ES2017 등은 무엇을 이야기할까요?
    ES5, ES6, ES2016, ES2017 등은 모두 ECMAScript 언어의 버전을 가리키는 용어
    ECMAScript는 European Computer Manufacturers Association의 약어로, 이 기구는 1997년에 자바스크립트를 표준화하기 위한 작업을 시작했다.

  - 자바스크립트의 표준은 어떻게 제정될까요?
    자바스크립트 언어의 표준은 ECMAScript 명세서를 제정된다.
    ECMAScript 명세서는 매년마다 새로운 버전이 발표되며, 이 버전들은 ECMAScript 5, ECMAScript 6, ECMAScript 2016, ECMAScript 2017 등으로 불린다. 이러한 버전들은 각각 새로운 기능, 구문, API 등을 도입하여 자바스크립트 언어를 발전한다.

- 자바스크립트의 문법은 다른 언어들과 비교해 어떤 특징이 있을까요?
  동적 타이핑(Dynamic Typing)
  자바스크립트는 변수의 타입을 미리 선언하지 않아도 된다. 대신 변수에 값이 할당될 때 타입이 자동으로 결정된다. 이러한 특징은 코드를 더 유연하게 만들어주지만, 타입 에러가 발생할 가능성도 높아진다.
  함수형 프로그래밍(Functional Programming)
  자바스크립트는 함수를 일급 객체(First-Class Object)로 다룬다. 이는 함수를 변수에 할당하거나, 다른 함수의 인자로 전달하거나, 함수를 반환할 수 있다는 것을 의미다. 이러한 특징을 이용하여 함수형 프로그래밍을 구현할 수 있다.
  클로저(Closure)
  자바스크립트에서 함수는 스코프(Scope)를 가진다. 이 스코프는 함수가 선언된 위치에 따라 결정되며, 함수는 자신의 스코프와 외부 스코프에 있는 변수들에 접근할 수 있다. 이러한 특징을 이용하여 클로저(Closure)를 구현할 수 있다.
  프로토타입 기반 상속(Prototype-based Inheritance)
  자바스크립트는 클래스(Class)를 지원하지 않는다. 대신 객체(Object)를 기반으로 상속을 구현한다. 객체는 다른 객체를 상속받을 수 있으며, 이를 프로토타입 기반 상속(Prototype-based Inheritance)이라고 한다.
  콜백(Callback)
  자바스크립트에서는 비동기 처리를 위해 콜백(Callback) 함수를 사용한다. 이는 함수를 다른 함수의 인자로 전달하여, 해당 함수가 처리 완료되면 콜백 함수를 호출하는 방식이다. 이를 통해 비동기적인 작업을 처리할 수 있다.

  - 자바스크립트에서 반복문을 돌리는 방법은 어떤 것들이 있을까요?
    1. for 문, 가장 일반적인 반복문으로, 조건문과 함께 사용하여 반복을 제어
    2. while 문, 조건식이 참인 동안 코드 블록을 반복 실행
    3. do-while 문, while 문과 비슷하지만, 코드 블록을 먼저 한 번 실행하고, 그 다음에 조건식을 대조한다.
    4. for...in 문, 객체의 속성을 반복해서 열거
    5. for...of 문, ES6에서 추가된 반복문으로, 배열과 같은 iterable 객체의 요소를 반복해서 열거한다.

- 자바스크립트를 통해 DOM 객체에 CSS Class를 주거나 없애려면 어떻게 해야 하나요?

  1. classList 프로퍼티와 add(), remove(), toggle() 메서드를 사용하는 방법
     // 요소에 "new-class" 클래스를 추가하기
     document.getElementById("myElement").classList.add("new-class");
     // 요소에서 "old-class" 클래스를 제거하기
     document.getElementById("myElement").classList.remove("old-class");
     // 요소에 "toggle-class" 클래스를 toggle() 메서드를 사용하여 추가하거나 제거하기
     document.getElementById("myElement").classList.toggle("toggle-class");
  2. className 프로퍼티를 사용하는 방법
     // 요소의 클래스에 "new-class" 클래스를 추가하기
     document.getElementById("myElement").className += " new-class";

  // 요소의 클래스에서 "old-class" 클래스를 제거하기
  document.getElementById("myElement").className =
  document.getElementById("myElement").className.replace("old-class", "");

  // 요소의 클래스에 "toggle-class" 클래스를 추가하거나 제거하기
  if (document.getElementById("myElement").className.indexOf("toggle-class") === -1) {
  document.getElementById("myElement").className += " toggle-class";
  } else {
  document.getElementById("myElement").className =
  document.getElementById("myElement").className.replace("toggle-class", "");
  }

  - IE9나 그 이전의 옛날 브라우저들에서는 어떻게 해야 하나요?
    classList 속성이 지원하지 않기 때문에 className을 이용한다.

- 자바스크립트의 변수가 유효한 범위는 어떻게 결정되나요?
  전역 범위(Global scope): 함수 안이나 블록 안에 들어가지 않은 변수는 전역 범위에 속한다. 전역 변수는 프로그램 어디에서나 접근할 수 있다.
  함수 범위(Function scope): 함수 내부에서 선언된 변수는 함수 범위에 속한다. 함수 내에서 선언된 변수는 함수 내에서만 접근할 수 있다.
  블록 범위(Block scope): ES6부터는 let과 const 키워드를 사용하여 블록 범위 변수를 선언할 수 있다. 블록 범위 변수는 중괄호({})로 둘러싸인 블록 내에서만 접근할 수 있다.

  - `var`과 `let`으로 변수를 정의하는 방법들은 어떻게 다르게 동작하나요?
    1. 유효 범위(Scope)의 차이
       var로 선언한 변수는 함수 스코프(Function scope)를 가진다.
       let으로 선언한 변수는 블록 스코프(Block scope)를 가진다.
    2. 중복 선언 허용 여부
       var로 선언한 변수는 같은 이름으로 중복 선언이 가능하다.
       let으로 선언한 변수는 같은 이름으로 중복 선언이 불가능하다.
    3. 호이스팅(Hoisting) 동작 여부
       var로 선언한 변수는 호이스팅이 일어난다. 즉, 변수를 선언하기 전에도 참조할 수 있다.
       let으로 선언한 변수는 호이스팅이 일어나지 않는다.
    4. 값 할당 시점의 차이
       var로 선언한 변수는 변수가 선언되기 전에 값을 할당할 수 있다. 선언 전에 값을 할당하면 변수의 값이 undefined가 된다.
       let으로 선언한 변수는 변수가 선언되기 전에 값을 할당할 수 없다. 선언 전에 값을 할당하면 에러가 발생한다.

- 자바스크립트의 익명 함수는 무엇인가요?
  자바스크립트에서 익명 함수는 이름이 없는 함수를 의미한다. 즉, 함수를 선언할 때 이름을 생략하고 직접 변수에 할당하는 방식으로 함수를 만드는 것을 말한다.
  var myFunc = function() {
  console.log("This is an anonymous function.");
  };

  - 자바스크립트의 Arrow function은 무엇일까요?
    ES6(2015)부터 추가된 Arrow function은 함수를 간략하게 표현할 수 있는 문법이다.
    익명 함수의 일종으로 함수의 내용이 단 한 줄인 경우 간단하게 표현할 수 있는 문법을 제공한다.

## Quest

- (Quest 03-1) 초보 프로그래머의 영원한 친구, 별찍기 프로그램입니다.
  - [이 그림](jsStars.png)과 같이, 입력한 숫자만큼 삼각형 모양으로 콘솔에 별을 그리는 퀘스트 입니다.
    - 줄 수를 입력받고 그 줄 수만큼 별을 그리면 됩니다. 위의 그림은 5를 입력받았을 때의 결과입니다.
  - `if`와 `for`와 `function`을 다양하게 써서 프로그래밍 하면 더 좋은 코드가 나올 수 있을까요?
  - 입력은 `prompt()` 함수를 통해 받을 수 있습니다.
  - 출력은 `console.log()` 함수를 통해 할 수 있습니다.
- (Quest 03-2) skeleton 디렉토리에 주어진 HTML을 조작하는 스크립트를 완성해 보세요.
  - 첫째 줄에 있는 사각형의 박스들을 클릭할 때마다 배경색이 노란색↔흰색으로 토글되어야 합니다.
  - 둘째 줄에 있는 사각형의 박스들을 클릭할 때마다 `enabled`라는 이름의 CSS Class가 클릭된 DOM 노드에 추가되거나 제거되어야 합니다.
- 구현에는 여러 가지 방법이 있으나, 다른 곳은 건드리지 않고 TODO 부분만 고치는 방향으로 하시는 것을 권장해 드립니다.

## Advanced

- Quest 03-1의 코드를 더 구조화하고, 중복을 제거하고, 각각의 코드 블록이 한 가지 일을 전문적으로 잘하게 하려면 어떻게 해야 할까요?
- Quest 03-2의 스켈레톤 코드에서 `let` 대신 `var`로 바뀐다면 어떤 식으로 구현할 수 있을까요?
