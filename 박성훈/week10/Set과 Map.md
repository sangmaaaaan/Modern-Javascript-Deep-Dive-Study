37장 Set과 Map
===

Set
---
- Set 객체는 중복되지 않는 유일한 값들의 집합이다.
- ![image](https://github.com/user-attachments/assets/80f9b915-bcd1-4f01-8e24-ae7ac4a8a833)

- Set 객체의 생성
  ```
  const set = new Set([1, 2, 3, 3]);
  console.log(set);  // Set(3) {1, 2, 3}
  ```
  - Set 생성자 함수로 생성한다. 인수를 전달하지 않으면 빈 객체가 생성된다.
  - Set 생성자 함수는 이터러블을 인수로 전달받아 Set 객체를 생성한다. 이때 이터러블의 중복된 값은 Set 객체에 요소로 저장되지 않는다.

- 요소 개수 확인
  ```
  const set = new Set([1, 2, 3]);
  console.log(set.Size);  // 3
  ```
  - Set 객체의 요소 개수를 확인할 때는 Set.prototype.size 프로퍼티를 사용한다.
  - getter 함수만 존재하는 접근자 프로퍼티므로 Set 객체의 요소 개수을 변경할 수 없다.
 
- 요소 추가
  ```
  const set = new Set();

  set.add(1).add(2).add(2);
  console.log(set);  // Set(2) {1,2}
  ```
  - Set 객체에 요소를 추가할 때는 Set.prototype.add 메서드를 사용한다.
  - add 메서드는 새로운 요소가 추가된 Set 객체를 반환한다. 따라서 연속 호출이 가능하다.
  - 중복된 요소의 추가는 무시한다. 일치 비교 연산자 ===가 다르다고 평가하는 NaN과 NaN, +0과 -0을 같다고 평가하여 중복 추가를 무시한다.
  - Set 객체는 객체나 배열과 같이 모든 값을 요소로 저장할 수 있다.

- 요소 존재 여부 확인
  ```
  const set = new Set([1, 2, 3]);
  console.log(set.has(2));  // true
  console.log(set.has(4));  // false
  ```
  - Set 객체에 특정 요소가 존재하는지 확인하려면 Set.prototype.has 메서드를 사용한다.
  - has 메서드는 특정 요소의 존재 여부를 나타내는 불리언 값을 반환한다.

- 요소 삭제
  ```
  const set = new Set([1, 2, 3]);

  set.delete(2);
  console.log(set);  // Set(2) {1, 3}
  ```
  - Set 객체의 특정 요소를 삭제하려면 Set.prototype.delete 메서드를 사용한다.
  - delete 메서드는 삭제 성공 여부를 나타내는 불리언 값을 반환한다. 따라서 연속 호출이 불가하다.
  - Set 객체는 인덱스를 갖지 않으므로 delete 메서드에 인덱스가 아닌 삭제하려는 요소값을 인수로 전달한다.
  - 존재하지 않는 요소를 삭제하려 하면 에러 없이 무시한다.

- 요소 일괄 삭제
  ```
  const set = new Set([1, 2, 3]);

  set.clear();
  console.log(set);  // Set(0) {}
  ```
  - Set 객체의 모든 요소를 일괄 삭제하려면 Set.prototype.clear 메서드를 사용한다.
  - clear 메서드는 언제나 undefined를 반환한다.

- 요소 순회
  ```
  const set = new Set([1, 2, 3]);

  set.forEach((v, v2, set) => console.log(v, v2, set));
  /*
  1 1 set(3) {1, 2, 3}
  2 2 set(3) {1, 2, 3}
  3 3 set(3) {1, 2, 3}
  */

  for (const value of set) {
    console.log(value);  // 1 2 3
  }

  console.log([...set]);  // [1, 2, 3]
  ```
  - Set 객체의 요소를 순회하려면 Set.prototype.forEach 메서드를 사용한다.
  - Set.prototype.forEach 메서드는 Array.prototype.forEach 메서드와 유사하게 콜백 함수와 forEach 메서드의 콜백 함수 내부에서 this로 사용될 객체를 인수로 전달한다.
  - Array.prototype.forEach 메서드와 인터페이스를 통일하기 위해 첫 번째 인수와 두 번째 인수로 같은 값인 현재 순회 중인 요소값을 받고, 세 번째 인수로 현재 순회 중인 Set 객체 자체를 받는다.
  - Set 객체는 이터러블이므로 for ... of 문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링의 대상이 될 수도 있다.
  - Set 객체는 요소의 순서에 의미를 갖지 않지만 Set 객체를 순회하는 순서는 요소가 추가된 순서를 따른다.

- 집합 연산
  - 교집합
    ```
    Set prototype.intersection
    ```
