![image](https://github.com/user-attachments/assets/bf6ec464-5bca-4f1b-a07c-59460de81537)43장 Ajax
===

Ajax란?
---
- Ajax(Asyncronous Javascript and XML)란 자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신하는 프로그래밍 방식을 말한다. Ajax는 브라우저에서 제공하는 Web API인 XMLHttpRequest 객체를 기반으로 동작한다. XMLHttpRequest는 HTTP 비동기 통신을 위한 메서드와 프로퍼티를 제공한다.
- 이전의 웹페이지는 html 태그로 시작해서 html 태그로 끝나는 완전한 HTML을 서버로부터 전송받아 웹페이지 전체를 처음부터 다시 렌더링하는 방식으로 동작했다. 따라서 화면이 전환되면 새로운 HTML을 받아 웹페이지 전체를 처음부터 다시 렌더링했다.
  - 이러한 전통 방식을 다음과 같은 단점이 있다.
    - 이전 웹페이지가 차이가 없어 변경할 필요가 없는 부분까지 다시 전송받기 때문에 불필요한 데이터 통신 발생
    - 변경할 필요 없는 부분까지 다시 렌더링. 이로 인해 화면 전환 시 화면이 순간적으로 깜빡이는 현상 발생
    - 클라이언트와 서버와의 통신이 동기 방식으로 동작하기 때문에 서버로부터 응답이 있을 때까지 다음 처리는 블로킹됨
- Ajax의 등장으로 서버로부터 비동기 방식으로 필요한 데이터만 전송받아 렌더링할 수 있게 되었다. 이를 통해 브라우저에서도 빠른 퍼포먼스와 부드러운 화면 전환이 가능해졌다.
  - Ajax는 전통적인 방식과 비교했을 때 다음과 같은 장점이 있다.
    - 변경할 부분을 갱신하는데 필요한 데이터만 서버로부터 전송받기 때문에 불필요한 데이터 통신이 발생하지 않는다.
    - 변경할 필요가 없는 부분은 다시 렌더링하지 않는다. 따라서 화면이 순간적으로 깜빡이는 형상이 발생하지 않는다.
    - 클라이언트와 서버의 통신이 비동기 방식으로 동작하기 때문에 서버에 요청을 보낸 후 블로킹이 발생하지 않는다.
   
JSON
---
- JSON(JavaScipt Object Notation)은 클라이언트와 서버 간의 HTTP 통신을 위한 텍스트 데이터 포맷이다. JS에 종속되지 않는 언어 독립형 데이터 포맷으로 대부분 프로그래밍 언어에서 사용할 수 있다.
- JSON 표기 방식
  - JSON은 JS의 객체 리터럴과 유사하게 키와 값으로 구성된 순수한 텍스트다. 키는 반드시 큰따옴표로 묶어야 하며, 값은 객체 리터럴과 같은 표기법을 그대로 사용할 수 있다. 하지만 문자열은 반드시 큰따옴표로 묶어야 한다.
- JSON.stringify
  - JSON.stringify 메서드는 객체를 JSON 포맷의 문자열로 변환한다.
  - 클라이언트가 서버로 객체를 전송하려면 객체를 문자열화해야 하는데 이를 직렬화라 한다.
  - JSON.stringify 메서드는 객체뿐만 아니라 배열도 변환한다.
 - JSON.parse
   - JSON.parse 메서드는 JSON 포맷의 문자열을 객체로 변환한다.
   - 서버로부터 클라이언트에 전송된 JSON 데이터는 문자열, 이를 객체로 사용하려면 문자열을 객체화해야 하는데 이를 역직렬화라 한다.
   - 배열이 JSON 포맷으로 변환되어 있는 경우 배열 객체로 변환한다. 배열 요소가 객체인 경우 배열의 요소까지 객체로 변환한다.
  
 XMLHttpRequest
 ---
- 브라우저는 주소창이나 HTML의 form 태그, a 태그를 통해 HTTP 요청 전송 기능을 제공한다. JS를 사용해 HTTP 요청을 전송하려면 XMLHttpRequest 객체를 사용한다. Web API인 XMLHttpRequest 객체는 HTTP 요청 전송과 응답 수신을 위한 다양한 메서드와 프로퍼티를 제공한다.

- XMLHttpRequest 객체 생성
  - ``` const xhr = new XMLHttpRequest(); ```
  - XMLHttpRequest 객체는 XMLHttpRequest 생성자 함수를 호출하여 생성한다. XMLHttpRequest는 브라우저 환경에서만 정상적으로 실행된다.

- XMLHttpRequest 객체의 프로퍼티와 메서드
  - ![image](https://github.com/user-attachments/assets/ed84efb7-10c0-4a03-b67d-44d55ead484f)
  - ![image](https://github.com/user-attachments/assets/1375f00e-ccb1-4586-a975-4dbda525caca)
  - ![image](https://github.com/user-attachments/assets/f6443390-ba8b-40e9-addd-ecf4f4258602)
  - ![image](https://github.com/user-attachments/assets/15c0c302-48d2-43ac-9429-8642bac5337c)
 
- HTTP 요청 전송
  - 다음과 같은 순서를 따른다.
    - XMLHttpRequest.prototype.open 메서드로 HTTP 요청을 초기화한다.
    - 필요에 따라 XMLHttpRequest.ptototype.setRequestHeader 메서드로 특정 HTTP 요청의 헤더 값을 설정한다.
    - XMLHttpRequest.prototype.send 메서드로 HTTP 요청을 전송한다.
  ```
  // XMLHttpRequest 객체 생성
  const xhr = new XMLHttpRequest();

  // HTTP 요청 초기화
  xhr.open('GET', '/users');

  // HTTP 요청 헤더 설정, 서버로 전송한 데이터 MIME 타입 지정(json)
  xhr.setRequestHeader('content-type', 'application/json');

  // HTTP 요청 전송
  xhr.send();
  ```

  - XMLHttpRequest.prototype.open
    - ``` xhr.open(method, url[, async]) ```
    - ![image](https://github.com/user-attachments/assets/013ee7f3-8387-49d1-95af-d4ca601df201)

    - open 메서드는 서버에 전송한 HTTP 요청을 초기화한다.
    - HTTP 요청 메서드는 클라이언트가 서버에게 요청의 종류와 목적을 알리는 방법으로 5가지 요청 메서드를 사용해 CRUD를 구현한다.
    - ![image](https://github.com/user-attachments/assets/d81cc591-9acb-425c-aa8f-cb554dc6799a)
   
  - XMLHttpRequest.prototypr.send
    - send 메서드는 open 메서드로 초기화된 요청을 서버에 전송한다. 서버로 전송하는 데이터는 GET, POST 요청 메서드에 따라 전송 방식에 차이가 있다
      - GET 요청 메서드의 경우 데이터를 URL의 일부분인 쿼리 문자열로 서버에 전송한다.
      - POST 요청 메서드의경우 데이터를 req.body에 담아 전송한다.
    - send 메서드에는 request body에 담아 전송할 데이터를 인수로 전달할 수 있다. 전송할 데이터가 객체인 경우 반드시 JSON.Stringify 메서드를 사용해 직렬화한 다음 전달해야 한다.
    - HTTP 요청 메서드가 GET인 경우 send 메서드에 페이로드로 전달한 인수는 무시되고 requset body는 null로 설정된다.
   
  - XMLHttpRequest.prototype.setRequestHeader
    - setRequestHeader 메서드는 특정 HTTP 요청의 헤더 값을 설정한다. setRequestHeader 메서드는 반드시 open 메서드를 호출한 이후 호출해야 한다.
      - Content-type은 request body에 담아 전송할 데이터의 MIME 타입의 정보를 표현한다.
        - ``` xhr.setRequestHeader('content-type', 'application/json'); ```
      - ![image](https://github.com/user-attachments/assets/65408835-d167-4b2a-b223-ba58e6b9af74)
      - 
    - HTTP 클라이언트가 서버에 요청할 때 서버가 응답할 데이터의 MIME 타입을 Accept로 지정할 수 있다.
      - ``` xhr.setRequestHeader('accept', 'application/json'); ```
    - Accpet 헤더를 설정하지 않으면 send 메서드가 호출될 때 accpet 헤더가 */*로 전송된다.
   
- HTTP 응답 처리
  - 서버가 전송한 응답을 처리하려면 XMLHttpRequest 객체가 발생시키는 이벤트를 캐치해야 한다. XMLHttpRequest 객체가 갖는 이벤트 핸들러 프로퍼티 중 HTTP 요청의 현재 상태를 나타내는 readyState 프로퍼티 값이 변경된 경우 발생하는 readystatechange 이벤트를 캐치하여 HTTP 응답을 처리할 수 있다.
  - XMLHttpRequest는 Web API이므로 반드시 브라우저 환경에서 실행해야 한다.
  - send 메서드를 통해 HTTP 요청을 서버에 전송하면 서버는 응답을 반환한다. 그러나 응답이 클라이언트에 언제 도달할지 알 수 없다. 따라서 readystatechange 이벤트를 통해 HTTP 요청의 현재 상태를 확인한다. 이 이벤트는 readyState 프로퍼티가 변경될 대마다 발생한다.
  - onreadystatechange 이벤트 핸들러 프로퍼티에 할당한 이벤트 핸들러는 readyState가 XMLHttpRequest.DONE인지 확인하여 응답이 완료되었는지 확인한다.
  - 응답이 완료되면 HTTP 요청에 대한 응답 상태를 나타내는 status가 200인지 확인해 에러 처리를 구분한다. 정상이라면 요청에 대한 request body를 나타내는 response에서 데이터를 취득한다.
  - readystatechange 이벤트 대신 load 이벤트를 캐치해도 된다. 이 이벤트는 HTTP 요청이 성공적으로 완료된 경우 발생한다. 따라서 이 경우 readyState가 DONE인지 확인할 필요가 없다.
