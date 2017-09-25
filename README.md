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

  이번에는 Ann에 대해서 이야기 해보겠습니다. 2년전, Ann은 웹과 cloud 기반의 응용프로그램을 주전공으로 소프트웨어 개발 학위를 받았습니다. 그녀는 iOS와 Android에서도 작동하는 모바일 응용프로그램과 더불어, 최근의 Model-view-controller 프레임워크를 기반으로 한 몇몇의 그다지 크지 않은 크기의 어플리케이션을 개발하였습니다. 그녀는 리눅스, 윈도우즈, OSX에서 작동하는 데스트탑 어플리케이션을 만들었고, 심지어 그 어플리케이션들을 전체적으로 cloud 기반으로한 서버리스 버전을 만들기 시작했습니다. *그리고 그 모든 것들이 자바스크립트로 이루어졌습니다.*
  <br />
  그것은 정말 대단한 것입니다! Bob이 10년동안 5가지의 개발 언어로 한 것을, Ann은 2년만에 *오직 자바스크립트만으로* 해낸 것입니다. 컴퓨터 역사상 특정 지식이 수많은 도메인에 쉽게 적용되고 유용했던 적은 드물었습니다.
  <br />
  1995년, 자그마한 열흘짜리 프르젝트가 이제는 세상에서 가장 널리 사용되는 프로그래밍 언어가 되었습니다. 자바스크립트는 강력한 자바스크립트 엔진과 단순한 웹 페이지를 넘어서게 해준 Node, Apache Cordova, Ionic, Electron과 같은 프레임 워크의 도입으로 인해 말 그대로 *어디에서나* 볼 수 있습니다. 그리고, HTML과 마찬가지로 언어 자체가 최신 어플리케이션 개발에 더욱 적합한 자바스크립트를 만들기 위해 대량의 업그레이드가 진행 중입니다.
  <br />
  이 책에서는, 여러분이 자바스크립트에 대해 알아야할 모든 정보를 알려드릴 것입니다. 그리하여 Ann이나 Bob과 같이, 여러분은 green field이건 brown field이건 상관없이 모든 종류의 어플리케이션을 개발할 수 있을 것입니다.

---
체크포인트
- Babel과 Traceur를 알고 있습니까? 알고 있다면 그것들이 최근의 자바스크립트 개발자들에게 왜 중요합니까?
- 웹 어플리케이션이 사용하는 브라우저의 자바스크립트 API의 핵심 부분들은 무엇입니까?
---

### 1.1 자바스크립트 언어의 이해 <a name="understanding-the-javascript-language"></a>

**[⬆ back to top](#table-of-contents)**
