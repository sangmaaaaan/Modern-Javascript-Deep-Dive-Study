# 37 - Map과 Set

## **37.1 Set**

![Untitled](37%20-%20Map%E1%84%80%E1%85%AA%20Set%20ab466adab9444ff184bef7af6576446a/Untitled.png)

### 37.1.1 Set 객체의 생성

- set객체는 set생성자 함수로 생성한다.
- set생성자 함수에 인수를 전달하지 않으면 빈 set객체가 생성된다.
- set생성자 함수는 **이터러블을 인수로 전달**받아 set객체를 생성한다
    - 이때 이터러블의 중복된 값은 set객체에 요소로 저장되지 않는다.

![Untitled](37%20-%20Map%E1%84%80%E1%85%AA%20Set%20ab466adab9444ff184bef7af6576446a/Untitled%201.png)

![Untitled](37%20-%20Map%E1%84%80%E1%85%AA%20Set%20ab466adab9444ff184bef7af6576446a/Untitled%202.png)

### **37.1.2 요소 개수 확인**

- `set.prototype.size`를 사용한다

### **37.1.3 요소 추가**

- `set.prototype.add`를 사용한다

### **37.1.4 요소 존재 여부 확인**

- `set.prototype.has` → 불리언 반환

### **37.1.5 요소 삭제**

- `set.prototype.delete`

### **37.1.6. 요소 일괄 삭제**

- `set.prototype.clear` → undefined반환

### 37.1.7 요소 순회

- `set`객체의 요소를 순회하려면 `set.prototype.forEach`메서드를 사용한다.
- `set.prototype.forEach` 메서드와 유사하기 `forEach`메서드의 콜백 함수 내부에서 `this`로 사용될 객채(옵션)을 인수로 전달한다 이때 콜백함수는 다음과 같이 3개의 인수를 전달한다.
    - **첫번째요소** : 현재 순회 중인 요소값
    - **두번쨰요소** : 현재 순회 중인 요소값
    - **세번째요소** : 현재 순회 중인`set`객체 자체

set은 이터러블이다.

- for...of문으로 순회할 수 있다
- 스프레드 문법과 배열 디스트럭처링의 대상이 될 수도 있다.

## **37.2 Map**

![Untitled](37%20-%20Map%E1%84%80%E1%85%AA%20Set%20ab466adab9444ff184bef7af6576446a/Untitled%203.png)

### 37.2.1 Map 객체의 생성

- map객체는 map 생성자 함수로 생성한다.
- map 생성자 함수에 인수를 전달하지 않으면 빈 map객체가 생성된다.
- **map생성자 함수는 이터러블을 인수로 전달받아 map객체를 생성한다.**
    - **이때 인수로 전달되는 이터러블은 `키와 값의 쌍`으로 이루어진 요소로 구성되어야 한다.**

### **37.2.2 요소 개수 확인**

- `map.prototype.size`
- size 변경 불가

### **37.2.3 요소 추가**

- `map.prototype.set`
- `set` 메서드는 새로운 요소가 추가된 `map` 객체를 반환한다.

### **37.2.4 요소 취득**

- `map.prototype.get`
- 값이 있으면 키를 갖는 값을 반환 , 없으면 undefined반환

### **37.2.5 요소 존재 여부 확인**

- `set.prototype.has`  → 불리언 반환

### 37.2.6 요소 삭제

- `set.prototype.delete`  → 성공 삭제 불리언 반환 , 요소가 없으면 무시됨

### **37.2.7. 요소 일괄 삭제**

- `set.prototype.clear`  → 언제나 undefined 반환

### 37.1.7 요소 순회

- `map`객체의 요소를 순회하려면 `set.prototype.forEach`메서드를 사용한다.
- `set.prototype.forEach` 메서드와 유사하기 `forEach`메서드의 콜백 함수 내부에서 `this`로 사용될 객채(옵션)을 인수로 전달한다 이때 콜백함수는 다음과 같이 3개의 인수를 전달한다.
    - **첫번째요소** : 현재 순회 중인 요소값
    - **두번쨰요소** : 현재 순회 중인 요소값
    - **세번째요소** : 현재 순회 중인`map`객체 자체

map 이터러블이다.

- for...of문으로 순회할 수 있다
- 스프레드 문법과 배열 디스트럭처링의 대상이 될 수도 있다