# this

## this 키워드는 왜 중요할까?

- 객체지향 프로그래밍에서 this는 중요한 개념
- 동작을 나타내는 메서드는 자신이 속한 객체의 상태(프로퍼티)를 참조하고 변경할 수있어야 한다.
- 이때 자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다.

## this 키워드가 왜 필요할까?

- 객체 리터럴 방식으로 생성한 객체의 경우, 메서드 내부에서 자신이 속한 객체를 가리키는 식별자를 재귀적으로 참조하는 과정을 통해 this 없이도 가능하다.
- But, 자기 자신이 속한 객체를 재귀적으로 참조하는 방식은 바람직하지 않음
- 생성자 함수를 통해 객체를 정의하는 경우, 생성자 함수를 정의하는 시점에서는 아직 인스턴스를 생성하기 전이기 때문에 생성자 함수가 생성할 인스턴스를 가리키는 식별자를 알 수 없다.
- 따라서 **‘this’키워드**를 통해 자신이 생성할 인스턴스를 가리키는 **자기 참조 변수**를 만듦

## this는 호출될 때 결정된다고?

<aside>
📌 자바스크립트에서 this는 함수가 호출되는 방식에 따라 this가 달라진다. === 동적으로 결정된다.

</aside>

- 일반 함수 호출
- 메서드 호출
- 생성자 함수 호출
- Function.prototype.apply/call/bind 메서드에 의한 간접 호출

## 일반 함수로 호출되면 무조건 전역객체 바인딩…!

<aside>
📌 어떤 함수라도 일반 함수로 호출된다면 this는 기본적으로 전역 객체가 바인딩 된다.

</aside>

- 일반적으로 this는 자기 참조 변수로, 자기 자신을 참조하기 위한 변수인데 인스턴스를 생성하지 않는 일반 함수에서는 ‘this’가 의미가 없다.
- 따라서 일반 함수 내에서 this는 전역 객체(window)를 가리킨다.
- strict mode가 적용된다면 undefined가 바인딩된다

```jsx
var value = 1;
const obj = {
  value: 100,
  foo() {
    console.log(this); // { value: 100, foo: f }
    setTimeout(function () {
      console.log(this); // window
      console.log(this.value); // 1
    }, 100);
  },
};
```

- 위의 예시에서 ‘setTimeout’의 콜백함수로 일반함수를 넘겼기 때문에, 일반함수에서 ‘this’는 무조건 전역 객체를 가리킨다는 것을 확인할 수 있다.

## 메서드 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩!

<aside>
📌 메서드 내부에서는 메서드 이름 앞의 마침표 연산자 앞에 기술한 객체가 바인딩된다. 
주의할 것은 메서드를 소유한 객체가 아닌 **메서드를 호출한 객체에 바인딩**된다는 것!

</aside>

```jsx
const anotherStudy = {
  name: "Algorithm Study",
  getName() {
    return this.name;
  },
};
const currentStudy = {
  name: "Modern DeepDive JavaScript",
};
currentStudy.getName = anotherStudy.getName;
// 메서드를 호출한 객체를 참조합니다.
// (.) 앞에 있는 객체에 집중
console.log(currentStudy.getName()); // Modern DeepDive JavaScript
const getName = anotherStudy.getName;
// getName 함수를 메서드로 호출한 것이 아니라, 일반 함수로 호출
console.log(getName()); // ''
// 일반 함수는 무조건 전역 객체를 바인딩하니까, window.name을 출력하지만 없으니 빈칸 출력
```

## 생성자 함수 호출은 미래에 생성할 인스턴스가 바인딩

<aside>
📌 생성자 함수 내부의 this에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩된다.

</aside>

```jsx
fucntion Study(name){
	//생성자 함수 내부의 this에는 생성자 함수가 생성할 인스턴스를 가리킨다.
	this.name = name;
	this.getName = function() {
		return this.name;
	};
	}
	
	const AlgorithmStudy = new Study("Algorithm Study");
	
	const ModernDeepDiveJavaScriptStudy = new Study("Modern DeepDive JavaScript");
	
	console.log(AlgorithmStudy.getName()); // Algorithm Study"
	console.log(ModernDeepDiveJavaScriptStudy.getName()); //Modern DeepDive JavaScript"
```

## apply, call, bind 메서드에 의한 간접 호출? 이게 뭔데??

![스크린샷 2024-07-09 오후 3.10.26.png](this%20329491e03c3443b6b29e620b565c803c/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-07-09_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.10.26.png)

- 기본적으로 apply, call, bind 모두  Function.prototype의 메서드로 모든 함수가 상속받아 사용할 수 있다.
- apply와 call은 호출할 함수에 인수를 전달하는 방식만 다를뿐 함수를 호출한다는 면에서는 동일하게 동작함.
- apply와 call 메서드는 보통 **`arguments`**와 같은 유사 배열 객체에 배열 메서드를 사용하고 싶을 때 사용할  수 있다.

### ‘call’과 ‘apply’를 사용하지 않았을 경우(추가 조사)

<aside>
📌 유사 배열 객체인 `arguments`를 직접 조작하려고 할 때, 배열 메서드를 사용할 수 없어서 오류가 발생

</aside>

```jsx
function exampleWithoutCallApply() {
  console.log(arguments); // [Arguments] { '0': 1, '1': 2, '2': 3 }

  // 배열 메서드를 직접 사용하려고 하면 오류 발생
  try {
    arguments.push(4); // TypeError: arguments.push is not a function
  } catch (e) {
    console.error(e.message); // "arguments.push is not a function"
  }

  // slice 메서드도 직접 사용할 수 없습니다.
  try {
    var args = arguments.slice(1); // TypeError: arguments.slice is not a function
  } catch (e) {
    console.error(e.message); // "arguments.slice is not a function"
  }
}

exampleWithoutCallApply(1, 2, 3);

```

### ‘call’과 ‘apply’를 사용할 경우(추가 조사)

<aside>
📌 `call`과 `apply`를 사용하여 유사 배열 객체를 배열로 변환하거나 배열 메서드를 사용 가능해짐

</aside>

```jsx
function exampleWithCallApply() {
  console.log(arguments); // [Arguments] { '0': 1, '1': 2, '2': 3 }

  // call을 사용해 slice 메서드를 arguments에 적용하여 배열로 변환
  var args = Array.prototype.slice.call(arguments);
  console.log(args); // [1, 2, 3]

  // 이제 배열 메서드를 사용할 수 있습니다.
  args.push(4);
  console.log(args); // [1, 2, 3, 4]

  // apply를 사용해 push 메서드를 arguments에 직접 적용
  Array.prototype.push.apply(arguments, [5]);
  console.log(arguments); // [Arguments] { '0': 1, '1': 2, '2': 3, '3': 5 }
}

exampleWithCallApply(1, 2, 3);
```

## 그럼 언제 사용할 수 있는데?(추가 조사)

1. 유사 배열객체를 배열로 변환
    
    ```jsx
    function example() {
      // arguments를 배열로 변환
      var args = Array.prototype.slice.call(arguments);
      console.log(args); // [1, 2, 3]
    }
    
    example(1, 2, 3);
    ```
    
2. 다른 객체에 배열 메서드 적용
    
    ```jsx
    var obj = {
      0: 'a',
      1: 'b',
      2: 'c',
      length: 3
    };
    
    // 배열의 slice 메서드를 사용해 객체의 일부분을 배열로 변환
    var arr = Array.prototype.slice.call(obj, 1);
    console.log(arr); // ['b', 'c']
    
    ```
    
3. 함수 인자의 동적 적용
    
    ```jsx
    function sum(a, b, c) {
      return a + b + c;
    }
    
    var numbers = [1, 2, 3];
    var result = sum.apply(null, numbers);
    console.log(result); // 6
    ```
    
4. this 컨텍스트 변경
    
    ```jsx
    var person1 = {
      name: 'Sangmin',
      greet: function(message) {
        console.log(message + ', ' + this.name);
      }
    };
    
    var person2 = {
      name: 'Beomsu'
    };
    
    // person1의 greet 메서드를 person2의 this로 호출
    person1.greet.call(person2, 'Hello'); // Hello, Beomsu
    ```
    
5. 상속 및 클래스 구조에서 활용
    
    <aside>
    📌 클래스 상속 구조에서 부모 클래스의 생성자를 자식 클래스에서 호출할 때 `call`을 사용할 수 있다.
    
    </aside>
    
    ```jsx
    function Person(name) {
      this.name = name;
    }
    
    function Student(name, grade) {
      Person.call(this, name); // 부모 클래스의 생성자 호출
      this.grade = grade;
    }
    
    var student = new Student('Sangmin', 'A');
    console.log(student.name); // Sangmin
    console.log(student.grade); // A
    ```
    
6. 최적화된 반복
    
    ```jsx
    var numbers = [5, 6, 2, 3, 7];
    var max = Math.max.apply(null, numbers); // 배열의 최대값 찾기
    console.log(max); // 7
    ```
    

## bind는 this로 사용할 객체만 전달

<aside>
📌 apply, call과 다르게 bind는 함수를 실행시키지 않고, this 객체만 전달한다.

</aside>

### ‘bind’를 사용하지 않았을 때 예시

```jsx
<!DOCTYPE html>
<html>
<head>
  <title>Bind Example</title>
</head>
<body>
  <button id="myButton1">Click me (no bind)</button>

  <script>
    var obj = {
      name: 'Sagnmin',
      handleClick: function() {
        console.log('Button clicked by ' + this.name);
      }
    };

    var button1 = document.getElementById('myButton1');

    // 이벤트 핸들러에 this를 obj로 고정하지 않음
    button1.addEventListener('click', obj.handleClick);
  </script>
</body>
</html>
```

```jsx
//결과 : Button clicked by undefined
```

- 버튼을 클릭하면 `obj.handleClick` 메서드가 호출
- 이벤트 핸들러로서 호출될 때 `this`는 이벤트를 트리거한 요소인 버튼 요소 (`button1`)를 가리킴
- 따라서 `this.name`은 `button1` 요소의 `name` 프로퍼티를 찾으려 하지만, 버튼 요소에는 `name` 프로퍼티가 정의되어 있지 않기 때문에 `undefined`가 할당됨
- 결과적으로 콘솔에 `Button clicked by undefined`가 출력

### ‘bind’를 사용했을 때 예시

```jsx
<!DOCTYPE html>
<html>
<head>
  <title>Bind Example</title>
</head>
<body>
  <button id="myButton2">Click me (with bind)</button>

  <script>
    var obj = {
      name: 'Sangmin',
      handleClick: function() {
        console.log('Button clicked by ' + this.name);
      }
    };

    var button2 = document.getElementById('myButton2');

    // 이벤트 핸들러에 this를 obj로 고정
    button2.addEventListener('click', obj.handleClick.bind(obj));
  </script>
</body>
</html>

```

```jsx
// 결과 : Button clicked by Sangmin
```

- 여기서는 `bind` 메서드를 사용하여 `handleClick` 메서드의 `this`를 `obj`로 고정
- `obj.handleClick.bind(obj)`는 `this`가 항상 `obj`를 가리키는 새로운 함수를 반환
- 버튼을 클릭하면 `bind`로 인해 `handleClick` 메서드 내부의 `this`는 `obj`를 가리키게 됨
- 결과적으로 ‘Button clicked by Sangmin’이 출력됨

## this를 예측할 수 없는 경우도 있을까?(추가조사)

- 일단 기본적으로 this는 함수가 호출될 결정된다고 말했다.
- 아래 예제의 답은 무엇일까요?
    
    ```jsx
    onst header = document.querySelector("header");
    header.addEventListener("click", function () {
      console.log(this); // 뭐가 될 것 같나요?
    });
    ```
    
- 정답 보기
    
    ![헤더.gif](this%20329491e03c3443b6b29e620b565c803c/%25E1%2584%2592%25E1%2585%25A6%25E1%2584%2583%25E1%2585%25A5.gif)
    
- 위의 코드는 **`addEventListener`** 내부적으로 동작하는 방식에 의해서 **`addEventListener`**를 호출한 객체가 할당됨
- 하지만 이것은 **`addEventListener`**가 이렇게 동작한다고 명시되어있는 [**문서**](https://developer.mozilla.org/ko/docs/Web/API/EventTarget/addEventListener#%EC%9D%B4%EB%B2%A4%ED%8A%B8_%EC%88%98%EC%8B%A0%EA%B8%B0_%EB%82%B4%EB%B6%80%EC%9D%98_this_%EA%B0%92)에서 보아서 알 수 있는거지 우리가 분석할 수 있는 것은 아니다.

## this를 예측가능하게 하려면 화살표함수로 콜백함수를 넘기자

```jsx
header.addEventListener("click", () => {
  console.log(this); // window
});
```

- 부모 스코프를 결정할 땐 "호출"이 아닌 "선언" 할 때 입니다.
- 스코프가 결정나는 것은 "호출"이 아니라 "선언"이기 때문이다.
- 화살표 함수를 "선언" 할 때의 부모는 **`anonymous`**입니다. 그렇기 때문에 **`anonymous`**의 **`this`**는 **`window`**가 되는 것이다.
- 따라서 위의 경우 화살표 함수의 "부모" 스코프가 this가 된다.

## 결론

- this함수는 일반함수로 호출되면 일반적으로 전역객체 바인딩
- apply, call, bind메서드에 의한 간접 호출
- 동적으로 결정되기 때문에 예측하지 못하는 경우도 있다.
- this를 예측가능하게 하려면 화살표함수를 사용할 수 있다.