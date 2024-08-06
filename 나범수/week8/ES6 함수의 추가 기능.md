# ES6 함수의 추가 기능

태그: 26장

# 함수의 구분

ES6 이전의 함수는 동일한 함수라도 다양한 형태로 호출할 수 있었다.

```jsx
var foo = function () {
  return 1;
};

// 일반적인 함수로서 호출
foo(); // 1

// 생성자 함수로서 호출
new foo(); // foo {}

// 메서드로서 호출
var obj = { foo: foo };
obj.foo();
```

`ES6 이전의 모든 함수는 일반 함수로서 호출할 수 있는 것은 물론 생성자 함수로서 호출할 수 있다.` 

| ES6 함수의 구분 | constructor | prototype | super | arguments |
| --- | --- | --- | --- | --- |
| 일반 함수 | O | O | X | O |
| 메서드 | X | X | O | O |
| 화살표 함수 | X | X | X | X |

일반 함수는 ES6이전과 별 차이가 없지만 메서드와 화살표 함수는 명확한 차이가 있다.

# 메서드

일반적으로 메서든는 객체에 바인딩된 함수를 일컫는 의미로 사용되었다. `ES6 사양에서 메서드는 메서드 축약 표현으로 정의된 함수만을 의미한다`

```jsx
const obj = {
  x: 1,
  // foo는 메서드다.
  foo() {
    return this.x;
  },
  // bar에 바인딩된 함수는 메서드가 아닌 일반 함수다.
  bar: function () {
    return this.x;
  },
};

console.log(obj.foo()); // 1
console.log(obj.bar()); // 1
```

`ES6 사양에서 정의한 메서드는 인스턴스를 생성할 수 없는 non-constructor다.` 따라서 ES6 메서드는 생성자 함수로서 호출할 수 없다.

```jsx
new obj.foo(); // typeError
new obj.bar(); // bar {}
```

⇒ 인스턴스를 생성할 수 없으므로 prototype  프로퍼티가 없고 프로토타입도 생성하지 않는다.

`ES6 메서드는 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 갖는다.` super 참조는 내부 슬롯 [[HomeObject]]를 사용하여 수퍼클래스의 메서드를 참조하므로 내부 슬롯 [[HomeObject]]를 갖는 ES6 메서드는  super 키워드를 사용할 수 있다.

⇒ ES6 메서드가 아닌 함수는 super 키워드를 사용할 수 없다. ES6 메서드가 아닌 함수는 내부 슬롯 [[HomeObject]] 를 갖지 않기 때문이다.

# 화살표 함수

화살표 함수는 콜백 함수 내부에서 this가 전역 객체를 가리키는 문제를 해결하기 위한 대안으로 유용하다.

## 화살표 함수 정의

### 함수 정의

```jsx
const multiply = (x, y) => x * y;
multiply(2, 3); // 6
```

### 매개변수 선언

```jsx
const arrow = (x, y) => { .. } ;
```

매개변수가 한 개인 경우에는 소괄호를 생략할 수 있지만 매개변수가 없는 경우는 생략할 수 없다.

### 함수 몸체 정의

함수 몸체가 하나의 문으로 구성된다면 함수 몸체를 감싸는 중괄호 {}를 생략할 수 있다. 이때 함수 몸체 내부의 문이 값으로 평가될 수 있는 표현식인 문이라면 암묵적으로 반환된다.

```jsx
const power = x => x ** 2;
power(2); // 4

// 위 표현은 다음과 동일하다.
const power = x => { return ** 2; }
```

객체 리터럴을 반환하는 경우 객체 리터럴을 소괄호 ()로 감싸 주어야 한다.

화살표 함수도 일급 객체이므로 고차함수에 인수로 전달할 수 있다.

## 화살표 함수와 일반 함수의 차이

1. 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor다.
    
    ```jsx
    const Foo = () => {};
    // 화살표 함수는 생성자 함수로서 호출할 수 없다.
    new Foo(); // TypeError
    ```
    
    화살표 함수는 인스턴스를 생성할 수 없으므로 prototype 프로퍼티가 없고 프로토타입도 생성하지 않는다.
    
2. 중복된 매개변수 이름을 선언할 수 없다.
    
    일반 함수는 중복된 매개변수 이름을 선언해도 에러가 발생하지 않는다.
    
3. 화살표 함수는 함수 자체의 this, arguments, super, [new.target](http://new.target) 바인딩을 갖지 않는다..
    
    따라서 화살표 함수 내부에서 this, arguments, super, new.target을 참조하면 스코프 체인을 통해 사위 스코프의 this, arguments, super, new.target을 참조한다.
    

## this

화살표 함수의 this는 일반 함수의 this와 다르게 동작한다. 이는 콜백 함수 내부의 this가 외부 함수의 this와 다르기 때문에 발생하는 문제를 해결하기 위해 의도적으로 설계된 것이다.

`화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조한다. 이를 lexical this라 한다.`

## arguments

화살표 함수는 함수 자체의 arguments 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 arguments를 참조하면 this와 마찬가지로 상위 스코프의 arguments를 참조한다.

# Rest 파라미터

## 기본 문법

매개변수 앞에 … 을 붙여서 정의한 매개변수를 의미한다.

`Rest  파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받는다.`

```jsx
function foo(...rest) {
  // 매개변수 rest는 인수들의 목록을 배열로 전달받는 Rest 파라미터다.
  console.log(rest); // [1, 2, 3, 4, 5]
}

foo(1, 2, 3, 4, 5);
```

```jsx
function foo(parm, ...rest) {
  // 매개변수 rest는 인수들의 목록을 배열로 전달받는 Rest 파라미터다.
  console.log(parm); // 1
  console.log(rest); // [2, 3, 4, 5]
}

foo(1, 2, 3, 4, 5);

```

Rest 파라미터는 반드시 마지막 파라미터이어야 한다.

## Rest 파라미터와 argmuents 객체

arguments 객체는 배열이 아닌 유사 배열 객체이므로 배열 메서드를 사용하려면 Function.prototype.call이나 Function.prototype.apply 메서드를 사용해 arguments 객체를 배열로 변환해야 하는 번거로움이 있었다.

ES6에서는 rest 파라미터를 사용하여 기반 인자 함수의 인수 목록을 배열로 직접 전달받을 수 있다.

```jsx
function sum(...args) {
  // Rest 파라미터 args에는 배열 [1, 2, 3, 4, 5]가 할당된다.
  return args.reduce((pre, cur) => pre + cur, 0);
}
console.log(sum(1, 2, 3, 4, 5)); // 15
```

# 매개변수 기본값

```jsx
function sum(x, y) {
  // 인수가 전달되지 않아 매개변수의 값이 undefined인 경우 기본값을 할당한다.
  x = x || 0;
  y = y || 0;

  return x + y;
}

console.log(sum(1)); // 1
```

ES6에서 도입된 매개변수 기본값을 사용하면 함수 내에서 수행하던 인수 체크 및 초기화를 간소화할 수 있다.

```jsx
function sum(x = 0, y = 0) {
  return x + y;
}

console.log(sum(1)); // 1
```

매개변수 기본값은 매개변수에 인수를 전달하지 않은 경우와 undefined를 전달한 경우에만 유효하다.