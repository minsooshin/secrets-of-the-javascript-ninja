<a name="building-the-page-at-runtime"></a>
## 2. 실행 시간에 페이지 구축하기

> 이번 장에서 다루어질 내용은
> - 웹 애플리케이션의 라이프사이클 단계들
> - 웹 페이지를 만들기 위한 HTML 코드 처리
> - 자바크스립트 코드 실행 순서
> - 이베트를 통한 상호작용 생성
> - 이벤트 순환

  자바스크립트의 탐색은 클라이언트 웹 애플리케이션의 컨텍스트와 자바스크립트 코드가 실행되는 엔진인 브라우저에서 수행됩니다. 언어로써의 자바스크립트와 플랫폼으로써의 브라우저를 계속 탐색할 더 탄탄한 기반을 확보하기 위해서는 먼저 완전한 웹 애플리케이션의 라이프사이클, 특히 자바스크립트 코드가 어떻게 이 라이프사이클에 적용되는지를 이해해야만 합니다.
  <br />
  이번 장에서, 페이지가 요청되는 순간부터 사용자의 상호작용을 통하여 페이지가 닫히는 순간까지의 웹 애플리케이션 라이프 사이클을 알아볼 것 입니다. 우선, HTML 코드를 처리하여 어떻게 페이지가 만들어지는지 볼 것입니다. 그런 후에 페이지에 훨씬 더 많은 유동성을 부여하는 자바스크립트 코드의 실행에 촛점을 맞출 것입니다. 마지막으로 사용자의 행동에 반응하는 상호적인 애플리케이션을 개발하기 위해 어떻게 이벤트들이 다루어지는지를 보겠습니다.
  <br />
  이 과정에서, DOM(웹 페이지의 구조화된 표현식)이나 이벤트 순환(애플리케이션에서 어떻게 이벤트가 작동할지를 결정)과 같은 몇몇의 기본적인 웹 애플리케이션 개념들을 살펴보겠습니다.

---
체크포인트
- 브라우저는 항상 정확하게 주어진 HTML에 따라서 페이지를 생성합니까?
- 몇 개의 이벤트를 웹 애플리케이션은 한 번에 다룰 수 있습니까?
- 왜 브라우저는 이벤트들을 처리하기 위해서 이벤트 큐를 사용해야만 합니까?
---

<a name="the-lifecycle-overview">
### 2.1 라이프사이클 개요

  전형적인 클라이언트 웹 애플리케이션의 라이프사이클은 사용자가 브라우저의 주소창에 URL을 입력하거나 링크를 클릭함으로 시작합니다. 가령, 어떠한 용어를 찾아보기 위해 구글 홈페이지에 간다고 해보겠습니다. 아래의 그림 2.1의 왼쪽 위에 보여지듯이 www.google.com 이라는 URL을 입력할 것입니다.
  <br /><br />
  <img src="assets/figure2.1.png" width="512" height="522" alt="그림 2.1" />
  <caption>그림 2.1 클라이언트 웹 애플리케이션의 라이프사이클은 사용자가 웹사이트의 주소를 지정함으로 시작하고 사용자가 그 웹 페이지를 떠날 때 끝납니다. 이는 페이지 구축과 이벤트 처리의 두 단계로 이루어집니다.

  사용자를 대신하여, 브라우저는 요청을 처리하는(3) 서버에 전송 될 요청을 보내고(2), HTML, CSS, 그리고 자바스크립트 코드로 구성된 응답을 받습니다. 브라우저가 이 응답을 받는 순간에(4) 클라이언트 웹 애클리케이션이 진정으로 시작되는 것입니다.
  <br />
  클라이언트 웹 애플리케이션은 그래픽화된 사용자 인터페이스(GUI) 애플리케이션이기 때문에, 라이프사이클은 다른 GUI 애플리케이션들(표준의 데스크탑 애플리케이션이나 모바일 애플리케이션)과 비슷한 단계들을 따르고 다음의 두 단계를 수행합니다.

  1. *페이지 구축* -- 사용자 인터페이스를 설정합니다.
  2. *이벤트 처리* -- 이벤트 순환에 들어가서(5) 이벤트가 발생하기를 기다리고(6), 이벤트 처리기를 작동시킵니다.

  애플리케이션의 라이프사이클은 사용자가 웹 페이지를 닫거나 떠날 때 끝납니다(7).
  <br />
  이제 사용자가 마우스를 움직이거나 페이지를 클릭할 때마다 메시지를 출혁하는, 사용자의 행동에 반응하는 간단한 UI를 가진 웹 애플리케이션 예제를 살펴보겠습니다. 이번 장 전반에 걸쳐 이 애플리케이션을 사용할 것입니다.

  **리스트 2.1 이벤트에 반응하는 GUI를 가진 작은 웹 애플리케이션**
  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>웹 앱 라이프사이클</title>
      <style>
        #first { color: green; }
        #second { color: red; }
      </style>
    </head>
    <body>
      <ul id="first"></ul>

      <script>
        function addMessage(element, message) {
          var messageElement = document.createElement("li");
          messageElement.textContent = message;
          element.appendChild(messageElement);
        }

        var first = document.getElementById("first");
        addMessage(first, "페이지 로딩중");
      </script>

      <ul id="second"></ul>

      <script>
        document.body.addEventListener("mousemove", function() {
          var second = document.getElementById("second");
          addMessage(second, "이벤트: 마우스 움직임");
        });

        document.body.addEventListener("click", funciton() {
          var second = document.getElementById("second")
          addMessage(second, "이벤트: 클릭");
        });
      </script>
    </body>
  </html>
  ```

  리스트 2.1을 보면 이는 먼저 `first`와 `second`라는 id를 가진 엘리먼트들의 텍스트 색상을 지정하는 두개의 CSS 규칙을 정의하고 있습니다. 다름으로 `first` id를 가진 엘리먼트를 정의하ㅂ니다.

  ```html
  <ul id="fitst"></ul>
  ```

  다음으로, 새로운 리스트 엘리먼트를 생성하고 그것의 텍스트 내용을 설정하고 기존에 있는 엘리먼트에 덧붙이는 작업을 하는 `addMessage` 함수를 정의합니다:

  ```js
  function addMessage(element, message) {
    var messageElement = document.createElement("li");
    messageElement.textContent = message;
    element.appendChild(messageElement);
  }
  ```

  그런후에, `getElementById`라는 내장 메소드를 사용하여 문서에서 ID `first`를 가진 엘리먼트는 가져오고, 페이지가 로딩되고 있다는 것을 알려주는 메시지를 추가합니다.

  ```js
  var first = document.getElementById("first");
  addMessage(first, "페이지 로딩중");
  ```

  다음으로 웹 페이지의 `body`에 두 개의 이벤트를 붙여줍니다. 사용자가 마우스를 `addMessage` 함수를 호출하여 `second` 리스트 엘리먼트에 `"이벤트: 마우스 움직임"`이라는 메시지를 추가할 `mousemove` 이벤트 처리기부터 해보겠습니다:

  ```js
  document.body.addEventListener("mousemove", function() {
    var second = document.getElementById("second");
    addMessage(second, "이벤트: 마우스 움직임");
  })
  ```

  사용자가 페이지를 클릭할 때마다 `second` 리스트 엘리먼트에 "이벤트: 클리"이라는 메시지를 출력할 `click` 이벤트 처리기도 추가합니다.

  ```js
  document.body.addEventListener("click", function() {
    var second = document.getElementById("second");
    addMessage(second, "이벤트: 클릭");
  })
  ```

  이 애플리케이션의 실행 결과는 다음 그림 2.2에 보여지는 것과 같습니다.
  <img src="assets/figure2.2.png" width="325" height="180" alt="그림 2.2" />
  <caption>그림 2.2 리스트 2.1에서 작성된 코드를 실행하면, 사용자의 행동에 따라 메시지가 출력됩니다.
