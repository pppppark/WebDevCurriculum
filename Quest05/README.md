# Quest 05. OOP 특훈

## Introduction

- 이번 퀘스트에서는 바닐라 자바스크립트의 객체지향 프로그래밍을 조금 더 훈련해 보겠습니다.

## Topics

- Separation of Concerns
- 객체지향의 설계 원칙
  - SOLID 원칙
- Local Storage

## Resources

- [Separation of concerns](https://jonbellah.com/articles/separation-of-concerns/)
- [SOLID](https://en.wikipedia.org/wiki/SOLID)
- [객체지향 설계 5원칙](https://webdoli.tistory.com/210)
- [MDN - Local Storage](https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage)

## Checklist

- 관심사의 분리 원칙이란 무엇인가요? 웹에서는 이러한 원칙이 어떻게 적용되나요?
  관심사의 분리(Separation of Concerns) 원칙은 소프트웨어 설계에서 각각의 모듈이나 클래스가 하나의 기능에 집중하도록 설계되어야 함을 의미한다. 이 원칙은 모듈화된 설계를 촉진하여 코드의 재사용성, 유지보수성, 확장성 등을 높이는 효과가 있다.
  웹에서도 이러한 원칙이 적용된다. 일반적으로 웹 애플리케이션은 프론트엔드와 백엔드로 나누어져 있다. 이때 프론트엔드는 사용자 인터페이스(UI)와 관련된 로직을 처리하고, 백엔드는 데이터 저장, 처리, 검증 등과 관련된 로직을 처리한다.
  또한 프론트엔드에서도 관심사의 분리를 위해 MVC(Model-View-Controller), MVVM(Model-View-ViewModel), MVP(Model-View-Presenter) 등의 디자인 패턴을 사용한다. 이러한 패턴은 각각의 역할이 분리된 모듈화된 코드를 작성할 수 있도록 지원하며, 코드의 가독성과 유지보수성을 높일 수 있다.

- 객체지향의 SOLID 원칙이란 무엇인가요? 이 원칙을 구체적인 예를 들어 설명할 수 있나요?
  SOLID 원칙은 객체지향 프로그래밍에서 유지보수성, 재사용성, 확장성, 유연성을 높이기 위해 제시된 원칙들이다. SOLID는 다음과 같은 원칙들로 구성된다.

  1. 단일 책임 원칙 (Single Responsibility Principle, SRP)
     한 클래스는 단 하나의 책임을 가져야 한다는 원칙이다.
     예를 들어, 사용자 정보를 담당하는 클래스는 사용자 정보를 저장하거나 검색하는 책임만을 가져야 하며, 그 외의 기능은 다른 클래스에게 위임해야 한다.
  2. 개방-폐쇄 원칙 (Open-Closed Principle, OCP)
     소프트웨어 요소는 확장에는 열려 있어야 하고, 수정에는 닫혀 있어야 한다는 원칙이다.
     즉, 기존의 코드를 변경하지 않고도 새로운 기능을 추가할 수 있도록 설계되어야 한다.
  3. 리스코프 치환 원칙 (Liskov Substitution Principle, LSP)
     자식 클래스는 언제나 부모 클래스의 자리를 대체할 수 있어야 한다는 원칙이다.
     즉, 자식 클래스는 부모 클래스에서 정의한 메소드와 프로퍼티를 모두 지원해야 한다.
  4. 인터페이스 분리 원칙 (Interface Segregation Principle, ISP)
     클라이언트가 자신이 사용하지 않는 메소드에 의존하지 않아야 한다는 원칙이다.
     즉, 인터페이스는 클라이언트가 필요로 하는 기능에 대해서만 추상화되어야 한다.
  5. 의존 역전 원칙 (Dependency Inversion Principle, DIP)
     고차원 모듈은 저차원 모듈에 의존하면 안 되며, 추상화는 구체적인 사항에 의존하면 안 된다는 원칙이다.
     즉, 코드를 작성할 때 구체적인 구현이 아닌 추상화된 인터페이스에 의존해야 한다.

  예를 들어, SRP 원칙은 사용자 정보를 담당하는 클래스에서 로그인 기능을 구현하는 것이 잘못된 설계라는 것을 의미한다. OCP 원칙은 새로운 기능을 추가할 때 기존의 코드를 수정하지 않고 새로운 클래스를 만들어서 구현하는 것이 좋다는 것을 의미한다. LSP 원칙은 자식 클래스가 부모 클래스의 메소드와 프로퍼티를 모두 지원해야 한다는 것을 의미한다.

- 로컬 스토리지란 무엇인가요? 로컬 스토리지의 내용을 개발자 도구를 이용해 확인하려면 어떻게 해야 할까요?
  로컬 스토리지는 웹 브라우저에 데이터를 저장하는 방법 중 하나로, 키-값 쌍 형태로 데이터를 저장할 수 있다. 로컬 스토리지는 브라우저를 닫아도 데이터가 유지되며, 다른 탭이나 창에서도 접근할 수 있다.

  로컬 스토리지의 내용을 개발자 도구를 이용해 확인하려면, 브라우저의 개발자 도구에서 "Application" 탭을 선택하고, 좌측의 "Storage" 항목을 클릭합니다. "Local Storage" 섹션에서 저장된 데이터를 확인할 수 있다. 개발자 도구를 사용하지 않고, 자바스크립트 코드에서 직접 로컬 스토리지의 값을 가져오거나 변경할 수도 있다. 이를 위해서는 localStorage 객체를 사용한다. 예를 들어, 로컬 스토리지에 "name"이라는 키로 "Park"이라는 값을 저장하려면 다음과 같은 코드를 사용한다.

  localStorage.setItem("name", "Park");

  저장된 값을 가져오려면 localStorage.getItem() 메소드를 사용한다.

  const name = localStorage.getItem("name");
  console.log(name);

## Quest

- 외부 라이브러리나 프레임워크를 사용하지 않고, 자바스크립트를 이용하여 간단한 웹브라우저 기반의 텍스트 에디터를 만들어 보겠습니다.
  - 기본적으로 VSCode와 같이 탭을 이용해 여러 개의 파일을 동시에 편집할 수 있습니다.
  - 탭을 눌러 열려 있는 다른 파일을 편집할 수 있으며 탭을 언제든지 닫을 수 있습니다.
  - VSCode와 같이 새 파일, 로드, 저장, 다른 이름으로 저장 등의 기능을 가집니다. 저장은 웹 브라우저의 로컬 스토리지를 이용합니다.
  - VSCode와 같이 탭이 수정되었는데 저장되기 이전일 경우 이를 알려주는 인디케이터가 작동합니다.
  - 같은 이름의 파일을 저장할 경우 에러를 표시해야 합니다.
- 이번 퀘스트의 결과물은 앞으로의 많은 퀘스트에서 재사용되게 되니, 주의깊게 코드를 작성해 보세요!

## Advanced

- 웹 프론트엔드 개발에서 이러한 방식의 패턴을 더 일반화해서 정리할 수 있을까요? 이 퀘스트에서 각각의 클래스들이 공통적으로 수행하게 되는 일들에는 무엇이 있을까요?
