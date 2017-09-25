# Secrets of JavaScript Ninja 한글 번역

<a name="table-of-contents"></a>
목차

1. [자바스크립트는 어디에나 있다](#javascript-is-everywhere)
    1. [자바스크립트 언어의 이해](#understanding-the-javascript-language)
    2. [브라우저의 이해](#understanding-the-browser)
    3. [최신 기술의 응용](#using-current-best-practices)
    4. [기술 이동의 신장](#boosting-skill-transferability)
    5. [요약](#chapter-1-summary)

2. [실시간으로 페이지 구축하기](#building-the-page-at-runtime)
    1. 라이프사이클 개요
    2. 페이지 구축 단계
    3. 이벤트 처리
    4. 요약
    5. 예제

3. [초보를 위한 First-class 함수: 정의와 arguments(인수)](#first-class-functions-for-the-novice)
    1. 함수의 차이는 무엇인가?
    2. 객체로써 함수 이해
    3. 함수 선언
    4. Arguments(인수)와 함수의 Parameters(매개변수)
    5. 요약
    6. 예제

4. [장인이 되기 위한 함수: 함수 호출 이해](#functions-for-the-journeyman)
    1. 암시적 함수 parameters 사용
    2. 함수 호출
    3. 함수 contexts 문제 해결
    4. 요약
    5. 예제

5. [달인이 되기 위한 함수: closures와 scopes](#functions-for-the-master)
    1. Closure 이해
    2. Colusres의 실제 응용
    3. 실행 contexts 기반의 코드 실행 추적
    4. Lexical 환경에서 식별자 추적
    5. 자바스크립트 변수 타입의 이해
    6. Colsures 작동 원리 이해
    7. 요약
    8. 예제

6. [미래를 위한 함수: generators와 promises](#functions-for-the-future)
    1. Generators와 promises를 이용한 비동기식 코드의 변화
    2. Generator 함수 응용
    3. Promises 응용
    4. Generators와 promises의 병행
    5. 요약
    6. 예제

## 1. 자바스크립트는 어디에나 있다 <a name="javascript-is-everywhere"></a>

> 이 챕터에서 다루어질 내용은
> - 자바스크립트 언어의 핵심 기능
> - 자바스크립트 엔진의 핵심 품목
> - 자바스크립트 개발의 세가지 관행

  Bob의 이야기로 시작해보겠습니다. C++를 이용해서 데스크탑 응용프로그램을 어떻게 개발하는지를 수년간 공부한 후에, 그는 2000년대 초반에 소프트웨어 개발자로 졸업을 하고 사회에 나왔습니다. 그 당시, 웹은 막 번성기를 맞이하고 있었고, 누구나 다 다음의 Amazon이 되고 싶어했습니다. 그래서 그는 먼저 웹 개발을 배웠습니다.
  <br />
  그는 form 인증이나 심지어 동적인 페이지 시계들과 같은 복잡한 기능을 구현하기 위해 자바스크립트로 뿌려진 웹 페이지들을 동적으로 생성할 수 있도록 PHP를 공부했습니다. 2년이라는 시간이 흐르고, 스마트폰이 거대한 시장을 생성하는 트렌드가 되었습니다. Bob은 iOS와 Android에서 실행되는 앱을 만들기 위해 Object-C와 Java를 공부했습니다.
  <br />
  수년 동안 Bob은 유지 보수 및 확장을 해야하는 많은 성공적인 응용프로그램을 개발했습니다. 하지만 불행히도, 매일같이 다 다른언어와 프레임워크 사이를 오가면서 Bob은 지쳐갔습니다.

### 1.1 자바스크립트 언어의 이해 <a name="understanding-the-javascript-language"></a>

**[⬆ back to top](#table-of-contents)**
