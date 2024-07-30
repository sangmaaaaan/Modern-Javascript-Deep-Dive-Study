31장 RegExp
===

정규 표현식이란?
---
```
const tel = '010-1234-567팔';

const regExp = /^\d{3}-\d{4}-\d{4}$/;

regExp.test(tel);  // false
```
- 정규 표현식은 일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어로 패턴 매칭 기능을 제공한다.
- 패턴 매칭 기능은 특정 패턴과 일치하는 문자열을 검색하거나 추출, 치환할 수 있는 기능을 말한다.
- 정규 표현식을 사용하면 반복문과 조건문 없이 패턴을 간단히 체크할 수 있지만, 주석이나 공백을 허용하지 않고 여러 기호를 혼합해서 사용해 가독성이 좋지 않다.

정규 표현식의 생성
---
![image](https://github.com/user-attachments/assets/41180c7f-615b-4cdc-8549-6abdbccc3d8a)
```
const target = 'Is this all there is?';

const regExp = /is/i;  // 패턴: is, 플래그: i
// const regExp = new RegExp(/is/i);

regExp.test(target);  // true
```
- 정규 표현식 리터럴과 RegExp 생성자 함수를 사용할 수 있다. 일반적인 방법은 정규 표현식 리터럴을 사용하는 것이다.
- 정규 표현식 리터럴은 패턴과 플래그로 구성된다.


RegExp 메서드
---
- RegExp.prototype.exec
```
const target = 'Is this all there is?';
const regExp = /is/; 

regExp.exec(target);  // ["is", index: 5, input: "Is this all there is?", groups: undefined]
```
  - exec 메서드는 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 배열로 반환한다. 매칭 결과가 없는 경우 null을 반환한다.
  - exec 메서드는 문자열 내의 모든 패턴을 검색하는 g 플래그를 지정해도 첫 번째 매칭 결과만 반환한다.

- RegExp.prototype.test
  - test 메서드는 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 불리언 값으로 반환한다.

- String.prototype.match
```
const target = 'Is this all there is?';
const regExp = /is/; 

regExp.match(regExp);  // ["is", index: 5, input: "Is this all there is?", groups: undefined]
```
  - String 표준 빌트인 객체가 제공하는 match 메서드는 대상 문자열과 인수로 전달받은 정규 표현식과의 매칭 결과를 배열로 반환한다.
  - String 메서드는 문자열 내의 모든 패턴을 검색하는 g 플래그를 지정하면 모든 매칭 결과를 배열로 반환한다.

플래그
---
```
const target = 'Is this all there is?';

target.match(/is/);  // 대소문자 구분하여 한 번 검색

target.match(/is/i);  // 대소문자 구별하지 않고 한 번 검색

target.match(/is/g);  // 대소문자 구분하여 전역 검색

target.match(/is/ig);  // 대소문자 구별하지 않고 전역 검색
```
- 플래그는 정규 표현식의 검색 방식을 설정하기 위해 사용한다. 총 6개가 있고 그 중 3개의 플래그를 주로 사용한다.
  - i: Ignore case, 대소문자를 구별하지 않고 패턴을 검색한다.
  - g: Global, 대상 문자열 내에서 패턴과 일치하는 모든 문자열을 전역 검색한다.
  - m: Multi line, 문자열의 행이 바뀌더라도 패턴 검색을 계속한다.
- 플래그는 선택적으로 사용할 수 있고, 하나 이상의 플래그를 동시에 설정 가능하다. 문자열에 패턴 검색 매칭 대상이 1개 이상 존재해도 첫 번째 매칭 대상만 검색하고 종료한다.

패턴
---
- 정규 표현식의 패턴은 문자열의 일정한 규칙을 표현하기 위해 사용한다. /로 열고 닫으며 문자열의 따옴표는 생략한다. 문자열 내에 패턴과 일치하는 문자열이 존재할 때 정규 표현식과 매치한다고 표현한다.
- 문자열 검색
  ```
  const target = 'Is this all there is?';
  const regExp = /is/;
  
  regExp.test(target);  // true
  regExp.match(regExp);  
  ```
  - 패턴에 문자 또는 문자열을 지정하면 검색 대상 문자열에서 패턴으로 지정한 값을 검색한다.
- 임의의 문자열 검색
  ```
  const target = 'Is this all there is?';
  const regExp = /.../g;  // 임의의 3자리 문자열 전역 검색

  target.match(regExp);  // ["Is ", "thi", "s a", "ll ", "the", "re ", "is?"]
  ```
  - .은 임의의 문자 한 개를 의미한다. 문자의 내용은 무엇이든 상관없다.
- 반복 검색
  ```
  const target = 'A AA B BB Aa Bb AAA';
  const regExp = /A{1,2}/g;  // A가 최소 1번, 최대 2번 반복되는 문자열 전역 검색

  target.match(regExp);  // ["A ", "AA "A", "AA ", "A"]
  ```
  - {m,n}은 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열을 의미한다. (콤마 뒤에 공백이 있으면 정상 동작하지 않는다.)
  - {n}은 {n,n}과 같이 n번 반복되는 문자열을 의미한다.
  - {n,}은 최소 n번 이상 반복되는 문자열을 말한다.
  - +는 앞선 패턴이 최소 한 번 이상 반복되는 문자열을 의미한다. +는 {1,}과 같다.
  - ?는 앞선 패턴이 최대 한 번 이상 반복되는 문자열을 의미한다. ?는 {0,1}과 같다.
- OR 검색
  ```
  const target = 'A AA B BB Aa Bb AAA';
  const regExp = /A|B/g;  // A 또는 B 검색
  //const regExp2 = /A+|B+/g;  // A 또는 B가 한 번 이상 반복되는 문자열 검색
  const regExp2 = /[AB]+/g;
  const regExp3 = /[A-Z]+/g;  // A ~ Z가 한 번 이상 반복되는 문자열 검색
  const regExp4 = /[A-Za-z]+/g;  // A ~ Z, a ~ z가 한 번 이상 반복되는 문자열 검색
  // const regExp5 = /[0-9]+/g;  // 숫자 검색
  const regExp5 = /[\d]+/g; 

  target.match(regExp); // ["A", "AA", "B", "BB", "A", "B"]
  ```
  - |은 or의 의미를 갖는다.
  - 분해되지 않은 단어 레벨로 검색하기 위해서는 +를 함께 사용한다.
  - [] 내의 문자는 or로 동작한다.
  - 범위를 지정하려면 [] 내에 -를 사용한다.
  - \d는 숫자를 의미한다. \D는 숫자가 아닌 문자를 의미한다.
  - \w는 알파벳, 숫자, 언더스코어를 의미한다. \W는 알파벳, 숫자, 언더스코어가 아닌 문자를 의미한다.
- NOT 검색
  - [] 내의 ^는 not의 의미를 갖는다.
  - ex) const regExp = /[^0-9]+/g;  // 숫자를 제외한 문자열을 검색
- 시작 위치로 검색
  - [] 밖의 ^는 문자열의 시작을 의미한다.
  - ex) const regExp = /^https/; // https로 시작하는지 검사
- 마지막 위치로 검색
  - $는 문자열의 마지막을 의미한다.
  - ex) const regExp = /com$/;  // com으로 끝나는지 검사

자주 사용하는 정규 표현식
---
- 특정 단어로 시작하는지 검사
  ```
  const url = 'https://example.com';
  
  /^https?:\/\//.test(url);  // true, http:// 또는 htt[s://로 시작하는지 검사한다.
  ```
- 특정 단어로 끝나는지 검사
  ```
  const fileName = 'index.html';
  
  /html$/.test(fileName);  // true, html로 끝나는지 검사한다.
  ```
- 숫자로만 이루어진 문자열인지 검사
  ```
  const target = '12345';

  /^\d+$/.test(target);  // true, 숫자로만 이루어진 문자열인지 검사한다.
  ```
- 하나 이상의 공백으로 시작하는지 검사
  ```
  const target = ' HI';

  /^[\s]+/.test(target);  // true, 하나 이상의 공백으로 시작하는지 검사한다.
  ```
- 아이디로 사용 가능한지 검사
  ```
  const id = 'abc123';

  /^[A-Za-z0-9]{4,10}$/.test(id);  // true, 알파벳 대소문자 또는 숫자로 시작하고 끝나며 4~10자리인지 검사한다.
  ```
- 메일 주소 형식에 맞는지 검사
  ```
  const email = 'abc123@gmail.com';

  /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/.test(email);  // true
  ```
- 핸드폰 번호 형식에 맞는지 검사
  ```
  const phone = '010-1234-5678';
  
  /^\d{3}-\d{3,4}-\d{4}$/.test(phone);
  ```
- 특수 문자 포함 여부 검사
  ```
  const target = 'abc#123';

  (/[^A-Za-z0-9]/gi).test(target);
  ```






















