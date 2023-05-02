# Quest 02. CSS의 기초와 응용

## Introduction

- CSS는 Cascading StyleSheet의 약자입니다. 웹브라우저에 표시되는 HTML 문서의 스타일을 지정하는 (거의) 유일하지만 다루기 쉽지 않은 언어입니다. 이번 퀘스트를 통해 CSS의 기초적인 레이아웃 작성법을 알아볼 예정입니다.

## Topics

- CSS의 기초 문법과 적용 방법
  - Inline, `<style>`, `<link rel="stylesheet" href="...">`
- CSS 규칙의 우선순위
- 박스 모델과 레이아웃 요소
  - 박스 모델: `width`, `height`, `margin`, `padding`, `border`, `box-sizing`
  - `position`, `left`, `top`, `display`
  - CSS Flexbox와 Grid
- CSS 표준의 역사
- 브라우저별 Developer tools

## Resources

- [MDN - CSS](https://developer.mozilla.org/ko/docs/Web/CSS)
- [Centering in CSS: A Complete Guide](https://css-tricks.com/centering-css-complete-guide/)
- [A complete guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [그리드 레이아웃과 다른 레이아웃 방법과의 관계](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Grid_Layout/%EA%B7%B8%EB%A6%AC%EB%93%9C_%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83%EA%B3%BC_%EB%8B%A4%EB%A5%B8_%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83_%EB%B0%A9%EB%B2%95%EA%B3%BC%EC%9D%98_%EA%B4%80%EA%B3%84)

## Checklist

- CSS를 HTML에 적용하는 세 가지 방법은 무엇일까요?
  1. HTML 태그에 style을 추가하여 바로 적용시킨다.
  2. css파일을 만들어 각 태그별로 적용시켜 class를 이용한다.
  3. <style>태그를 이용해 HTML 문서 내에 작성한다.
  - 세 가지 방법 각각의 장단점은 무엇일까요?
    1번 방법은 즉각으로 수정하면서 확인가능하지만 HTML문서 내가 더러워진다.
    2번 방법은 css파일로 따로 관리하기 때문에 HTML 문서내 최적화가 된다.
    하지만 .div 형식으로 태그별로 지정해서 작성해야하기 때문에 다른 방법보다 복잡하다.
    3번 방법은 파일을 변환하지 않고 한 파일내에서 모든 것을 작성할 수 있다.
    반면에 HTML 문서가 너무 커지고 길어지는 단점이 있다.
- CSS 규칙의 우선순위는 어떻게 결정될까요?

  1. 속성 값 뒤에 !important 를 붙인 속성
  2. HTML에서 style을 직접 지정한 속성
  3. #id 로 지정한 속성
  4. .(class), :추상클래스 로 지정한 속성
  5. (태그)이름 으로 지정한 속성
  6. 상위 객체에 의해 상속된 속성

- CSS의 박스모델은 무엇일까요? 박스가 화면에서 차지하는 크기는 어떻게 결정될까요?
  콘텐츠 영역(content area)은 콘텐츠 경계(content edge)가 감싼 영역으로, 글이나 이미지, 비디오 등 요소의 실제 내용을 포함
  테두리 영역(border area)은 테두리 경계(border edge)가 감싼 영역으로, 안쪽 여백 영역을 요소의 테두리까지 포함하는 크기
  안쪽 여백 영역(패딩 영역, padding area)은 안쪽 여백 경계(padding edge)가 감싼 영역으로, 콘텐츠 영역을 요소의 안쪽 여백까지 포함하는 크기

- `float` 속성은 왜 좋지 않을까요?
  기본적으로 이미지 정렬을 위해 등장한 CSS 스타일이지만 레이아웃 정렬에도 많이 사용했다. 그렇기 때문에 불편한 사항들이 있다.
  overflow: visible인 경우, 부모 요소의 크기가 자동으로 늘어나지 않는다. (position: absolute와 비슷하게 렌더링)
  float속성은 clear하지 않는 이상 계속해서 상속이 된다.
  화면의 플로우와 코드의 플로우는 가능하면 동일한 것이 좋다. 하지만 float를 쓴다는 것은 화면에서 띄워 애초에 플로우를 무시한다.

- Flexbox(Flexible box)와 CSS Grid의 차이와 장단점은 무엇일까요?
  Flexbox는 기본적으로 1차원 레이아웃을 위해 만들어졌다. 로우나 컬럼 형태로 작동한다. Flexbox는 모든 방향으로 정렬이 가능하고, reverse도 가능하다. Container로 사용할 경우, 하위 item들을 정렬하기가 매우 수월하다. 단점으로는 퍼포먼스 이슈가 있다.
  Grid는 2차원 레이아웃을 위해 만들어졌다. prototyping할 때 매우 쉽고 효율적으로 간단하게 작성하여 2차원의 레이아웃을 관리할 수 있다. 반면에 모든 브라우저에서 지원하는 것이 아니다.
  Flexbox는 행과 열을 효율적으로 정렬하고 구성할 수 있어 레이아웃에 적합하지만 grid는 더욱 큰 단위로 구축할때 편하다.

- CSS의 비슷한 요소들을 어떤 식으로 정리할 수 있을까요?
  1. 선택자(Selectors): CSS에서 스타일을 적용하는 대상을 지정하는 방법으로, 요소의 이름, 클래스, ID 등을 이용하여 선택한다.
  2. 속성(Properties): CSS에서 스타일을 지정하는 방법으로, 텍스트 색상, 폰트, 배경색 등과 같은 스타일 속성들을 정의한다.
  3. 값(Values): CSS에서 속성에 적용할 값으로, 글꼴 크기, 마진, 패딩 등과 같은 값들을 지정한다.
  4. 단위(Units): CSS에서 값과 함께 사용되며, 크기, 거리, 시간 등의 측정 단위로 px, em, rem, % 등이 있다.
  5. 상태(Pseudo-classes): 선택자의 상태에 따라 스타일을 지정하는 방법으로, hover, active, focus 등의 상태에 대한 스타일을 정의
  6. 미디어(Media): 미디어 쿼리를 사용하여 뷰포트 크기에 따라 스타일을 변경하는 방법으로, 모바일 기기나 데스크톱 화면 등에 따라 다른 스타일을 지정할 수 있다.
  7. 변수(Variables): CSS 변수를 사용하여 스타일 속성에 대한 값을 정의하고, 이를 재사용할 수 있다.
     다음과 같은 방법으로 정리하면 이해하기 쉽고 유지보수가 쉽다.

## Quest

- Quest 01에서 만들었던 HTML을 바탕으로, [이 그림](screen.png)의 레이아웃과 CSS를 최대한 비슷하게 흉내내 보세요. 꼭 완벽히 정확할 필요는 없으나 align 등의 속성은 일치해야 합니다.
- **주의사항: 되도록이면 원래 페이지의 CSS를 참고하지 말고 아무것도 없는 백지에서 시작해 보도록 노력해 보세요!**

## Advanced

- 왜 CSS는 어려울까요?
- CSS의 어려움을 극복하기 위해 어떤 방법들이 제시되고 나왔을까요?
- CSS가 브라우저에 의해 해석되고 적용되기까지 내부적으로 어떤 과정을 거칠까요?
- 웹 폰트의 경우에는 브라우저 엔진 별로 어떤 과정을 통해 렌더링 될까요?
