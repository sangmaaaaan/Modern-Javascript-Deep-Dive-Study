# RegExp

태그: 31장

# 정규 표현식이란?

일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어다. 

자바스크립트 고유 문법이 아니며 대부분의 프로그래밍 언어와 코드 에디터에 내장되어 있다.

정규 표현식은 문자열을 대상으로 `패턴 매칭 기능`을 제공한다. 특정 패턴과 일치하는 문자열을 검색하거나 추출 또는 치환할 수 있는 기능을 말한다.

```jsx
const tel = "010-1234-567팔";

const regExp = /^\d{3}-\d{4}-\d{4}$/;

regExp.test(tel); // false
```

# 정규 표현식의 생성

정규 표현식 리터럴과 RegExp 생성자 함수를 사용할 수 있다.

- 정규 표현식 리터럴

![Untitled](RegExp%20bafbef76eebc41f0b378e24450785ee8/Untitled.png)

- 생성자 함수

```jsx
const regexp = new RegExp(/is/i);
```

# RegExp 메서드

## RegExp.prototype.exec

인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 배열로 반환한다.

```jsx
const target = "Is this all there is?";
const regExp = /is/;

regExp.exec(target); 
// [ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
```

## RegExp.prototype.test

인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 불리언 값으로 반환한다.

```jsx
const target = "Is this all there is?";
const regExp = /is/;

regExp.test(target); // true
```

## String.prototype.match

대상 문자열과 인수로 전달받은 정규 표현식과의 매칭 결과를 배열로 반환한다.

```jsx
const target = "Is this all there is?";
const regExp = /is/;

target.match(regExp);
// [ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
```

⇒ exec 메서드는 문자열 내의 모든 패턴을 검색하는 g 플래그를 지정해도 첫번째 매칭 결과만 반환한다. 하지만 String.prototype.match 메서드는 g 플래그가 지정되면 모든 매칭 결과를 배열로 반환한다.

# 플래그

패턴과 함께 정규 표현식을 구성하는 플래그는 정규 표현식의 검색 방식을 설정하기 위해 사용한다.

| 플래그 | 의미 | 설명 |
| --- | --- | --- |
| i | Ingore case  | 대소문자를 구별하지 않고 패턴을 검색한다. |
| g | Global | 대상 문자열 내에서 패턴과 일치하는 모든 문자열을 전역 검색한다. |
| m  | Multi line | 문자열의 행이 바뀌더라도 패턴 검색을 계속한다. |

```jsx
const target = "Is this all there is?";

// target 문자열에서 is 문자열을 대소문자를 구별하지 않고 한 번만 검색한다.
target.match(/is/i);
// [ 'Is', index: 0, input: 'Is this all there is?', groups: undefined ]
```

# 패턴

## 문자열 검색

정규 표현식의 패턴에 문자 또는 문자열을 지정하면 검색 대상 문자열에서 패턴으로 지정한 문자 또는 문자열을 검색한다.

## 임의의 문자열 검색

.은 임의의 문자 한 개를 의미한다.

```jsx
const target = "Is this all there is?";

// 임의의 3자리 문자열을 대소문자를 구별하여 전역 검색한다.
const regExp = /.../g;

console.log(target.match(regExp));
// [
//   'Is ', 'thi',
//   's a', 'll ',
//   'the', 're ',
//   'is?'
// ]

```

## 반복 검색

{m, n}은 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열을 의미한다. 콤마 뒤에 공백이 있으면 정삭 동작하지 않으므로 주의하기 바란다.

## OR 검색

|은 or의 의미를 갖는다

```jsx
const regExp = /A|B/g;
```