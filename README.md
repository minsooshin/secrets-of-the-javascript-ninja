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

<a name="javascript-is-everywhere"></a>
## 1. 자바스크립트는 어디에나 있다

> 이 챕터에서 다루어질 내용은
> - 자바스크립트 언어의 핵심 기능
> - 자바스크립트 엔진의 핵심 품목
> - 자바스크립트 개발의 세가지 관행

  Bob의 이야기로 시작해보겠습니다. C++를 이용해서 데스크탑 응용프로그램을 어떻게 개발하는지를 수년간 공부한 후에, 그는 2000년대 초반에 소프트웨어 개발자로 졸업을 하고 사회에 나왔습니다. 그 당시, 웹은 막 번성기를 맞이하고 있었고, 누구나 다 다음의 Amazon이 되고 싶어했습니다. 그래서 그는 먼저 웹 개발을 배웠습니다.
  <br />
  그는 form 인증이나 심지어 동적인 페이지 시계들과 같은 복잡한 기능을 구현하기 위해 자바스크립트로 뿌려진 웹 페이지들을 동적으로 생성할 수 있도록 PHP를 공부했습니다. 2년이라는 시간이 흐르고, 스마트폰이 거대한 시장을 생성하는 트렌드가 되었습니다. Bob은 iOS와 Android에서 실행되는 앱을 만들기 위해 Object-C와 Java를 공부했습니다.
  <br />
  수년 동안 Bob은 유지 보수 및 확장을 해야하는 많은 성공적인 응용프로그램을 개발했습니다. 하지만 불행히도, 매일같이 다 다른언어와 프레임워크 사이를 오가면서 Bob은 지쳐갔습니다.
  <br />
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

<a name="understanding-the-javascript-language"></a>
### 1.1 자바스크립트 언어의 이해

  경력이 쌓일수록, Bob이나 Ann과 같은 많은 자바스크립트 개발자들은 그 언어를 구성하는 방대한 수의 요소들을 적극적으로 사용하고 있습니다. 그러나, 많은 경우에 있어서, 그러한 기술들이 기초 단계를 넘어서지 못하고 있을지도 모릅니다. C와 같은 문법을 사용하는 자바스크립트는 C와 유사한 다른 언어(예를 들면, C#이나 자바)와 표면적 유사성을 가지므로 친숙하다는 인상을 남기기 때문에 이러한 현상이 발생할 수 있다고 여겨집니다.
  <br />
  사람들은 종종 그들이 C#이나 자바를 알면, 자바스크립트가 어떻게 작동하는지도 잘 안하고 착각합니다. 다은 주요 언어들과 비교해보면, 자바스크립트는 상당히 함수 지향적입니다. 몇몇의 자바스크립트 개념들은 대부분의 다른 언어들과 근본적으로 다릅니다.
  <br />
  이 차이점들은 아래의 내용들을 포함합니다:
  - 최우선 객체: 함수 -- 자바스크립트에서 함수는 다른 자바스크립트 객체들과 같이 다루어집니다. 이들은 리터럴을 통해 만들 수 있고 변수로 참조 되며 함수의 인수로도 전달 될 수 있고, 심지어 함수의 반환 값으로 사용 될 수도 있습니다. 3장에서 최우선 객체로써의 함수가 자바스크립트 코드에 가져다주는 훌륭한 이점들을 살펴볼 것입니다.
  - 함수 클로저 -- 함수 클로저 개념은 일반적으로 잘 이해하기가 쉽지 않습니다. 하지만 이는 근본적으로 자바스크립트에 있어서 함수가 얼마나 중요한지를 보여줍니다. 지금은 *함수가 자신 안에서 사용된 외부 변수를 능동적으로 유지(덮어쓰기)할 때 그 함수가 크로저* 라는 것을 아는 것으로 충분합니다. 5장에서 이에 대해 명확하게 다룰 것이므로 왜 클로저를 쓰는지 모른다고 해서 아직은 걱정할 필요 없습니다. 클로저뿐만 아니라 3장과 4장에서는 함수 자체의 수많은 특징들을, 그리고 5장에서는 식별자들의 범주에 대해서 살펴볼 것입니다.
  - 범주 -- 최근까지도, 자바스크립트는 (다름 C와 비슷한 어어들처럼)구간 변수라는 것이 없었습니다. 대신에, 전역 변수들과 함수 변수들에 의존해 왔습니다.
  - 프로토타입 기반의 객체 지향 -- 클래스 기반의 객채 지향을 사용하는 다른 주 언어들(C#, 자바나 Ruby)과는 달리, 자바스크립트는 프로토타입을 사용합니다. 종종 (자바같은) 클래스 기반의 언어에서 자바스크립트로 넘어온 개발자들은 자바처럼 자바스크립트를 사용하려고 합니다. 즉, 자바스크립트 문법을 이용하여 자바의 클래스 기반 코드를 짜려고 합니다. 그러고선, 몇 가지 이유에서 결과가 그들이 생각한 것과 달라놀라곤 합니다. 이것이 왜 프로토타입을 심층적으로 들여다 보려고 하는 이유입니다. 어떻게 프로토타입 기반의 객체 지향이 작동하고 어떻게 자바스크립트에서 실행되는지를 말입니다.

  자바스크립트는 객체와 프로토타입들, 함수와 클로저들간의 긴밀한 관계로 구성되어 있습니다. 이 개념들간의 관게를 이해하면 자바스크립트 코드가 웹 페이지, 데스크탑 앱, 모바일 앱, 서버등 어느곳에서 실행되던지 상관없이 어떠한 유형의 어플리케이션 개발에 대한 강력한 기반을 제공함으로써 자바스크립트 프로그래밍 능력이 크게 향상 될 것입니다.
  <br />
  이러한 기본적인 개념에 더해서, 다른 자바스크립트의 기능들도 더 좋고 실용적인 코드를 작성하는데 도움을 줄 것입니다. 이들 중 일부는 Bob과 같은 노련한 개발자가 자바나 C++와 같은 다른 언어에서 찾아볼 수 있는 기능입니다. 특히, 우리는 다음에 초점을 맞추고 있습니다:
  - Generators -- 요청에 의해 복수의 값을 생성하거나 요청간에 실행을 중지할 수 있는 함수
  - Promises -- 비동기식 코드에 더 나은 제어를 제공해 줌
  - Proxies -- 우리로 하여금 특정 객체에 대한 접근을 제어할 수 있게 해줌
  - Advanced array methods -- 배열을 보다 우수하게 다룰 수 있게 해줌
  - Maps and sets -- maps는 dictionary collections를 생성함, sets는 고유 아이템 집합을 다룰 때 용이함
  - Regular expressions -- 복잡한 코드 조각들을 명료하게 할 수 있음
  - Modules -- 코드를 비교적 작고 독립적인 조각으로 나누어 프로젝트를 관리하기 쉽게 만들 수 있음
  이러한 기본 사항을 깊이 이해하고 고급 언어 기능을 최대로 활요하면 코드를 상위 수준으로 향상시킬 수 있습니다. 이러한 개념과 기능을 함께 묶어 기술을 습득하면 모든 종류의 자바스크립트 어플리케이션을 손쉽게 만들 수 있습니다.

#### 1.1.1 자바스크립트는 어떻게 진화할 것인가?
  표준화를 담당하는 ECMAScript 위원회는 이제 막 자바스크립트의 ES7/ES2016 버전을 끝냈다. ES7은 자바스크립트에 있어서(최소한 ES6에 비교했을 때) 상대적으로 작은 업그레이드이다, 왜냐하면 위원회의 목표는 언어데 대해 작고, 매년 증가하는 변화에 집중하는 것이기 때문입니다.
  <br />
  이 책에서 우리는 ES6뿐만 아니라 비동기식 코드를 다루는데 도움이 될 새로운 비동기 함수와 같은 ES7 기능들도 살펴볼 것입니다.

  <img src="assets/es6.png" width="50" height="48" />
  <img src="assets/es7.png" width="54" height="48" />
  **NOTE**: ES6/ES2015 혹은 ES7/ES2016에 정의 되어있는 자바스크립트의 기능들을 다룰 때는, 이 아이콘이 브라우저에서 지원되는지 여부에 대한 링크와 함께 표시될 것입니다.

  언어 사양에 대한 매년 증가하는 업데이트는 대단히 좋은 소식입니다, 그러나 이것은 그 새로운 사양이 공개되고 웹 개발자들이 곧바로 이에 대한 접근권을 가지는 것을 의미하지는 않습니다. 자바스크립트 코드는 자바스크립트 엔진에 의해서 실행됩니다, 따라서 우리가 선호하는 자바스크립트 엔진들이 이러한 새롭고 기대되는 기능들과 잘 작동할 수 있도록 업데이틑 되기까지 기다려야합니다.
  <br />
  불행히도, 자바스크립트 엔진 개발자들이 항상 최선의 노력을 다하지만, 당신이 너무 사용하고 싶어하는 기능이 아직은 지원되지 않을 가능성이 언제나 있습니다.
  <br />
  다행히, 여러분은 이 리스트들을 통해서 다양한 브라우저의 기능 지원 상태를 확인할 수 있습니다: [https://kangax.github.io/compat-table/es6/](https://kangax.github.io/compat-table/es6/), [http://kangax.github.io/compat-table/es2016plus/](http://kangax.github.io/compat-table/es2016plus/), and [https://kangax.github.io/compat-table/esnext/](https://kangax.github.io/compat-table/esnext/).

**[⬆ back to top](#table-of-contents)**
