# Set과 Map

태그: 37장

# Set

`Set 객체는 중복되지 않는 유일한 값들의 집합이다.` Set 객체는 배열과 유사하지만 다음과 같은 차이가 있다.

| 구분 | 배열 | Set 객체 |
| --- | --- | --- |
| 동일한 값을 중복하여 포함할 수 있다. | O | X |
| 요소 순서에 의미가 있다. | O | X |
| 인덱스로 요소에 접근할 수 있다. | O | X |

## Set 객체의 생성

```jsx
const set = new Set();
console.log(set) // set(0) {}
```

Set 생성자 함수는 이터러블을 인수로 전달받아 Set 객체를 생성한다. 이때 이터러블의 중복된 값은 Set 객체에 요소로 저장되지 않는다.

```jsx
const set1 = new Set([1,2,3,3]);
console.log(set1) // set(3) {1, 2, 3}

const set2 = new Set("hello");
console.log(set2) // set(4) { "h", "e", "l", "o"}
```

## 요소 개수 확인

Set 객체의 요소 개수를 확인할 때는 Set.prototype.size 프로퍼티를 사용한다.

```jsx
const { size } = new Set([1,2,3,3]);
console.log(size); // 3
```

## 요소 추가

Set 객체에 요소를 추가할 때는 Set.prototype.add 메서드를 사용한다.)

```jsx
const set = new Set();
console.log(set); Set(0) {}

set.add(1);
console.log(set); Set(1) {1}
```

일치 비교 연산자 === 을 사용하면 NaN, NaN을 다르다고 평가한다. 하지만 Set 객체는 같다고 평가하여 중복 추가를 허용하지 않는다.

Set 객체는 객체나 배열과 같이 자바스크립트의 모든 값을 요소로 저장할 수 있다.

## 요소 존재 여부 확인

Set 객체에 특정 요소가 존재하는지 확인하려면 Set.prototype.has 메서드를 사용한다.

```jsx
const set = new Set([1, 2, 3]);

console.log(set.has(2)); // true
console.log(set.has(4)); // false
```

## 요소 삭제

Set 객체의 특정 요소를 삭제하려면 Set.prototype.delete 메서드를 사용한다. delete 메서드에는 인덱스가 아니라 삭제하려는 요소값을 인수로 전달해야 한다.

```jsx
const set = new Set([1, 2, 3]);

set.delete(2);
console.log(set); // Set(2) {1, 3}
```

## 요소 일괄 삭제

Set 객체의 모든 요소를 일괄 삭제하려면 Set.prototype.clear 메서드를 사용한다. 

```jsx
const set = new Set([1, 2, 3]);

set.clear();
console.log(set); // set(0) {}
```

## 요소 순회

Set 객체의 요소를 순회하려면 Set.prototype.forEach 메서드를 사용한다. Set.prototype.forEach 메서드는 Array.prototype.forEach 메서드와 유사하게 콜백 함수와 forEach 메서드의 콜백 함수 내부에서 this로 사용될 객체(옵션)를 인수로 전달한다.

- 첫 번째 인수: 현재 순회 중인 요소값
- 두 번째 인수: 현재 순회 중인 요소값
- 세 번재 인수: 현제 순회 중인 Set 객체 자체

```jsx
const set = new Set([1, 2, 3]);

set.forEach((v, v2, set) => console.log(v, v2, set));
/*
const set = new Set([1, 2, 3]);

set.forEach((v, v2, set) => console.log(v, v2, set));
1 1 Set(3) { 1, 2, 3 }
2 2 Set(3) { 1, 2, 3 }
3 3 Set(3) { 1, 2, 3 }
*/
```

`Set 객체는 이터러블이다.` 따라서 for … of 문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링의 대상이 될 수도 있다.

# Map

`Map 객체는 키와 값의 쌍으로 이루어진 컬렉션이다. Map 객체는 객체와 유사하지만 다음과 같은 차이가 있다.`

| 구분 | 객체 | Map 객체 |
| --- | --- | --- |
| 키로 사용할 수 있는 값 | 문자열 또는 심벌 값 | 객체를 포함한 모든 값 |
| 이터러블 | X | O |
| 요소 개수 확인 | Object.keys(obj).length | map.size |

## Map 객체의 생성

```jsx
const map = enw Map();
console.log(map); // Map(0) {}
```

`Map 생성자 함수는 이터러블을 인수로 전달받아 Map 객체를 생성한다. 이때 인수로 전달되는 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성되어야 한다.`

```jsx
const map1 = new Map([
  ["key1", "value1"],
  ["key2", "value2"],
]);
console.log(map1); //Map(2) { 'key1' => 'value1', 'key2' => 'value2' }

const map2 = new Map([1, 2]) // TypeError
```

## 요소 개수 확인

Map 객체의 요소 개수를 확인할 때는 Map,prototype.size 프로퍼티를 사용한다.

```jsx
const { size } = new Map([
  ["key1", "value1"],
  ["key2", "value2"],
]);
console.log(size); // 2
```

## 요소 추가

Map 객체에 요소를 추가할 때는 Map.prototype.set 메서드를 사용한다.

```jsx
const map = new Map();
console.log(map) // Map(0) {}

map.set("key1", "value1");
console.log(map); // Map(1) {"key1" => "value"}
```

일치 비교 연산자 === 을 사용하면 NaN, NaN을 다르다고 평가한다. 하지만 Map 객체는 같다고 평가하여 중복 추가를 허용하지 않는다.

객체는 문자열 또는 심벌 값만 키로 사용할 수 있지만 Map 객체는 키 타입에 제한이 없다.

## 요소 취득

Map 객체에서 특정 요소를 취득하려면 Map.prototype.get 메서드를 사용한다.

## 요소 존재 여부 확인

Map 객체에 특정 요소가 존재하는지 확인하려면 Map.prototype.has 메서드를 사용한다.

## 요소 삭제

Map 객체의 요소를 삭제하려면 Map.prototype.delete 메서드를 사용한다.