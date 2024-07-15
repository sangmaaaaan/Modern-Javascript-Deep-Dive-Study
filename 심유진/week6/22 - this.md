# 22 - this

## **22.1 this 키워드**

this를 통해 자신이 속한 객체 또는 생성할 인스턴스의 프로퍼티나 메소드를 참조 가능.

## 22.2.3 생성자 함수 호출

생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스에 바인딩된다.

```jsx
// 생성자 함수
function Circle(radius) {
  // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 반지름이 5인 Circle 객체를 생성
const circle1 = new Circle(5);
// 반지름이 10인 Circle 객체를 생성
const circle2 = new Circle(10);

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20
```

```jsx
// new 연산자와 함께 호출하지 않으면 생성자 함수로 동작하지 않는다. 즉, 일반적인 함수의 호출이다.
const circle3 = Circle(15);

// 일반 함수로 호출된 Circle에는 반환문이 없으므로 암묵적으로 undefined를 반환한다.
console.log(circle3); // undefined

// 일반 함수로 호출된 Circle 내부의 this는 전역 객체를 가리킨다.
console.log(radius); // 15
```

- 일반 함수 호출
    - 전역 객체에 바인딩.
- 메서드 호출
    - 메서드를 호출한 객체에 바인딩.
- 생성자 함수 호출
    - 생성자 함수가 생성할 인스턴스에 바인딩.
- call / apply / bind
    - 첫 번째 인수로 전달한 객체에 바인딩.