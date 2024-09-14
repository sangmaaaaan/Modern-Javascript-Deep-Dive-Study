# 43 - Ajax

## Ajax

JS를 사용해서 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신하는 프로그래밍 방식

Web Api인 XMLHttpRequest 객체를 기반으로 동작하며 이 객체는 HTTP 비동기 통신을 위한 메서드와 프로퍼티를 제공한다.

XMLHttpRequest

HTTP 비동기 통신

### Ajax 장점

• 필요한 데이터만 서버로부터 전송 받아서 효율적임,
• 변경할 필요가 없는 부분 재 랜더링하지 않음.
• 클라이언트와 서버의 통신이 비동기적으로 동작하여 요청을 보낸 후에 블로킹이 발생하지 않음.

---

## JSON

JSON은 클라이언트와 서버 간의 HTTP 통신을 위한 텍스트 데이터 포맷

키는 큰 따옴표 문자열 값도 큰 따옴표로 묶는 표기방식

`{`

`“이름” : “심유진”`

`}`

### JSON.Stringify

JSON 포맷의 문자열로 변환함

클라이언트가 서버로 객체를 **전송**하려면 객체를 문자열화 해야함 == 직렬화

`JSON.stringify(value[, replacer[, space]])`

value : JSON 문자열로 반환할 값

replacer - Optional : 문자열화 동작방식 변경 함수

space - Optional : 가독성을 목적으로 JSON 문자열 출력에 공백을 삽입하는데 사용되는 String 또는 Number 객체

- [ Number (1~10) : 스페이스 수 ]
- [ String : 문자열 수에 따른 공백 ]

### **JSON.parse**

JSON 포맷의 문자열을 객체로 변환함.

**서버로부터 받은** JSON 데이터를 객체로 사용하려면 필요 == 객체

`JSON.parse(text[, reviver])`

text : JSON으로 변환할 문자열.

## reviver - Optional : 함수라면, 변환 결과를 반환하기 전에 이 인수에 전달하여 변형

### XMLHtppRequest ( WebAPI )

JS를 사용하여 HTTP 요청을 전송하려면 XMLHttpRequest 객체를 사용하여 수행함.

`const xhr = new XMLHttpRequest();`

**XMLHttpRequest 객체의 프로토타입 프로퍼티 ( 요청 상태 , 응답 상태 , 요청의 응답 메세지 , 응답 타입 , 응답 몸체 )**

**XMLHttpRequest 객체의 이벤트 핸들러 프로퍼티 ( 프로퍼티 값 변경 , 요청 에러 , 요청 성공 )**

**XMLHttpRequest 객체의 메서드 ( 요청 초기화 , 요청 전송 , 요청 중단 , 요청 헤더값 설정 )**

**XMLHttpRequest 객체의 정적 프로퍼티 ( 서버 응답 완료 )**

| GET    | index/retrieve | 모든/특정 리소스 취득 |
| ------ | -------------- | --------------------- |
| POST   | create         | 리소스 생성           |
| PUT    | replace        | 리소스의 전체 교체    |
| PATCH  | modify         | 리소스의 일부 수정    |
| DELETE | delete         | 모든/특정 리소스 삭제 |

send 메서드는 open 메서드로 초기화된 HTTP 요청을 서버에 전송한다.

- GET 요청 메서드의 경우 데이터를 URL의 일부분인 **쿼리 문자열**로 서버에 전송한다.
- POST 요청 메서드의 경우 **데이터(페이로드)를 요청 몸체**에 담아 전송한다.

페이로드가 객체인 경우 반드시 JSON.stringify 메서드를 사용하여 직렬화한 다음 전달!

**XMLHttpRequest.prototype.setReuqestHeader**

특정 HTTP 요청의 헤더 값을 설정한다.

Content-type은 요청 몸체에 담아 전송할 데이터의 MIME 타입의 정보를 표현한다.

| MIME 타입   | 서브타입                                           |
| ----------- | -------------------------------------------------- |
| text        | text/plain, text/html, text/css, text,javascript   |
| application | application/json, application/x-www-form-urlencode |
| multipart   | multipart/formed-data                              |

HTTP 클라이언트가 서버에 요청할 때 서버가 응답할 데이터의 MIME 타입을 accept로 지정할 수 있다. 만약 설정되지 않으면 send 메서드 호출 시 `*/*` 로 설정
