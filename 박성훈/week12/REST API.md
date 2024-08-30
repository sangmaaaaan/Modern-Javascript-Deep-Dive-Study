44장 REST API
===

REST(REpresentational State Transfer)는 HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍처고, REST API는 REST를 기반으로 서비스 API를 구현한 것을 의미한다.

REST API의 구성
---
- REST API는 자원, 행위, 표현의 3가지 요소로 구성된다. REST는 자체 표현 구조로 구성되어 REST API만으로 HTTP 요청의 내용을 이해할 수 있다.
- ![image](https://github.com/user-attachments/assets/7f57e158-2336-4a73-a85c-f146e0859735)

REST API 설계 원칙
---
1. URI는 리소스를 표현해야 한다.
  - 리소스를 식별할 수 있는 이름은 동사보다는 명사를 사용한다. 따라서 get과 같은 행위에 대한 표현이 들어가선 안된다.
    ```
    # bad
    GET /getTodos/1
    GET /todos/show/1

    # good
    GET /todos/1
    ```
2. 리소스에 대한 행위는 HTTP 요청 메서드로 표현한다.
  - HTTP 요청 메서드는 클라이언트가 서버에게 요청의 종류와 목적을 알리는 방법이다. 주로 5가지 요청 메서드를 사용해 CRUD를 구현한다.
  - ![image](https://github.com/user-attachments/assets/d9ad7d9a-01cc-4eaf-8aa8-68b28490cbb2)

JSON Server를 이용한 REST API 실습
---
- JSON Server 설치 => 루트 폴더에 db.json 파일 생성 ==> JSON Server 실행 ==> GET / POST / PUT / PATCH / DELETE 요청
