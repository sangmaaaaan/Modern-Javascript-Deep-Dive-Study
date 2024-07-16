# this

태그: 22장

# this. 키워드

메서드가 자신이 속한 객체의 프로퍼티를 참조하려면 먼저 자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다.

하지만 자기 자신이 속한 객체를 재귀적으로 참조하는 방식은 일반적이지 않으며 바람직하지도 않다. 

```jsx
function Circle(radius) {
    //이 시점에는 생성자 함수 자신이 생성할 인스턴스를 가리키는 식별자를 알 수 없다.
    ????.radius = radius;
}

Circle.prototype.getDiameter = function() {
    //이 시점에는 생성자 함수 자신이 생성할 인스턴스를 가리키는 식별자를 알 수 없다.
    return 2 * ????.radius;
}

// 생성자 함수로 인스턴스를 생성하려면 먼저 생성자 함수를 정의해야 한다.
const circle = new Circle(5)
```

생성자 함수를 정의하는 시점에는 아직 인스턴스를 생성하기 이전이므로 생성자 함수가 생성할 인스턴스를 가리키는 식별자를 알 수 없다. 따라서 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 특수한 식별자가 필요하다. 이를 위해 this.라는 특수한 식별자를 제공한다.

this 는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.

함수를 호출하면 arguments객체와 tihs가 암묵적으로 함수 내부에 전달된다. this도 지역 변수처럼 사용할 수 있으나 this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.

<aside>
💡 this 바인딩
바인딩이란 식별자와 값을 연결하는 과정을 의미한다. 예를 들어 변수 선언은 변수 이름과 확보된 메모리 공간의 주소를 바인딩하는 것이다. this 바인딩은 this와 this가 가리킬 객체를 바인딩 하는 것이다.

</aside>

```jsx
const circle = {
    radius: 5,
    getDiameter() {
        // this는 메서드를 호출한 객체를 가리킨다.
        return 2 * this.radius;
    }
};

console.log(circle.getDiameter()) // 10
```

자바나 C++같은 클래스 기반 언어에서 this는 언제나 클래스가 생성하는 인스턴스를 가리킨다. 하지만 자바스크립트의 this는 함수가 호출되는 방식에 따라 this에 바인딩될 값, 즉 this 바인딩이 동적으로 결정된다.

this는 코드 어디에서든 참조가 가능하다. 전역에서도 함수 내부에서도 참조할 수 있다. 하지만 this는 객체의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수이므로 일반적으로 객체의 메서드 내부 또는 생성자 함수 내부에서만 의미가 있다. 따라서 strict mode가 적용된 일반 함수 내부의 this에는  undefined가 바인딩된다. 일반 함수 내부에서 this를 사용할 필요가 없기 때문이다.

# 함수 호출 방식과 this 바인딩

this 바인딩은 함수 호출 방식, 즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다.

## 일반 함수 호출

기본적으로 this에는 전역 객체가 바인딩된다.

```jsx
function foo() {
    console.log(this) ; //window
    function bar() {
        console.log(this) // window
    }
    bar();
}
foo();
```

전역함수는 물론이고 중첩 함수를 일반 함수로 호출하면 함수 내부의 this에는 전역 객체가 바인딩된다. 다만 객체를 생성하지 않는 일반 함수에서 this는 의미강 벗다. 

```jsx
var value = 1;

const obj = {
    value: 100,
    foo() {
        console.log(this) // {value: 100, foo: f}
        // 콜백 함수 내부의 this에는 전역 객체가 바인딩된다.
        setTimeout(function() {
            console.log(this) // window
            console.log(this.value) // 1
        }, 100)
    }
}

obj.foo()
```

이처럼 일반 함수로 호출된 모든 함수 (중첩 함수, 콜백 함수 포함) 내부의 this에는 전역 객체가 바인딩 된다.

또는 화살표 함수를 사용해서 this 바인딩을 일치시킬 수도 있다.

```jsx
var value = 1;

const obj = {
    value: 100,
    foo() {
        setTimeout(() => console.log(this.value), 100) // 100
     }
}

obj.foo()
```

## 메서드 호출

매서드 내부의 this에는 메서드를 호출한 객체, 즉 메서드를 호출할 때 메서드 이름 앞의 마침표 연산자 앞에 기술한 객체가 바인딩된다. 단 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다.

프로토타입 메서드 내부에서 사용된 this도 일반 메서드와 마찬가지로 해당 메서드를 호출한 객체에 바인딩된다.

```jsx
function Person(name) {
    this.name = name;
}
Person.prototype.getName = function () {
    return this.name;
}

const me = new Person("Lee");

// getName 메서드를 호출한 객체는 me다.
console.log(me.getName()) // Lee

Person.prototype.name = "Kim";

// getName 메서드를 호출한 객체는 Person.prototype이다.
console.log(Person.prototype.getName()) // Kim
```

## 생성자 함수 호출

일반 함수와 동일한 방법으로 생성자 함수를 정의하고 new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다. 만약 new 연산자와 함께 생성자 함수를 호출하지 않으면 생성자 함수가 아니라 일반 함수로 동작한다.