### ⭐️35 스프레드 문법

<aside>
🔅

→ ES6에서 도입된 스프레드 문법 … 은 하나로 뭉쳐 있는 여러 값들의 집합을 펼쳐서 개별적인 값들의 목록으로 만든다.

- 스프레드 문법을 사용할 수 있는 대상은 Array, String, Map, Set, DOM 컬렉션, arguments와 같이 for…of 문으로 순회할 수 있는 이터러블에 한정된다.

```jsx
// ...[1, 2, 3]은 [1, 2, 3]을 개별 요소로 분리한다.(-> 1, 2, 3)
console.log(...[1, 2, 3]); // 1 2 3

// 문자열은 이터러블이다.
console.log(... 'Hello'); // H e l l o

// Map과 Set은 이터러블이다.
console.log(...new Map([['a', '1'], ['b', '2']])); // [ 'a', '1' ] [ 'b', '2' ]
console.log(...new Set([1, 2, 3])); // 1 2 3

// 이터러블이 아닌 일반 객체는 스프레드 문법의 대상이 될 수 없다.
console.log(... { a: 1, b: 2 });
// TypeError
// 스프레드 문법의 결과는 변수에 할당할 수 없다.
const list = ...[1, 2, 3]; // SyntaxError: token...
```

→ 스프레드 문법의 결과물은 값으로 사용할 수 없고, 다음과 같이 쉼표로 구분한 값의 목록을 사용하는 문맥에서만 사용할 수 있다.

1. 함수 호출문의 인수 목록
2. 배열 리터럴의 요소 목록
3. 객체 리터럴의 프로퍼티 목록
</aside>

### ⭐️35.1 함수 호출문의 인수 목록에서 사용하는 경우

<aside>
🔅

→ 요소들의 집합인 배열을 펼쳐서 개별적인 값들의 목록으로 만든 후, 이를 함수의 인수 목록으로 전달해야 하는 경우가 있다.

```jsx
const arr = [1, 2, 3];

// 배열 arr의 요소 중에서 최대값을 구하기 위해 Math.max를 사용한다.
// max에다가 숫자가 아닌 배열을 인수로 저달하면 최대값을 구할 수 없어 NaN이다.
const max = Math.max(arr); // NaN

// 스프레드 문법이 제공되기 이전에는 배열을 펼쳐서 요소들의 목록에 인수로 전달하려
// apply 함수를 사용했다.
// apply 함수의 2번째 인수(배열)은 apply 함수가 호출하는 함수의 인수 목록이다.
// 따라서 배열이 펼쳐져서 인수로 전달되는 효과가 있다.
var max = Math.max.apply(null, arr); // -> 3

// 이때 스프레드 문법을 사용하면 더 간결하고 가독성이 좋다.
const max = Math.max(...arr); // -> 3

// 스프레드 문법은 앞에서 살펴본 Rest 파라미터와 형태가 동일하여 혼동할수도 있다.
// Rest 파라미터는 인수들의 목록을 배열로 전달받는다.
function foo(...rest) {
	console.log(rest); // 1, 2, 3 -> [1, 2, 3]
}

// 스프레드 문법은 배열과 같은 이터러블을 펼쳐서 개별적인 값들의 목록을 만든다.
// [1, 2, 3] -> 1, 2, 3
foo(...[1, 2, 3]);
```

</aside>

### ⭐️35.2 배열 리터럴 내부에서 사용하는 경우

<aside>
🔅

→ 스프레드 문법을 배열 리터렁에서 사용하면 ES5에서 사용하던 기존의 방식보다 더욱 간결하고 가독성 좋게 표현할 수 있다.

</aside>

### **📌 35.2.1 concat**

<aside>
🔅

→ ES5에서 2개의 배열을 1개의 배열로 결합하고 싶은 경우 배열 리터럴만으로 해결할 수 없고 concat 메서드를 사용해야 한다.

```jsx
// ES5
var arr = [1, 2].concat([3, 4]);
console.log(arr); // [1, 2, 3, 4]

// 스프레드 문법을 사용하여 배열 리터럴만으로 2개의 배열을 1개의 배열로 결합
// ES6
const arr = [...[1, 2], ...[3, 4]];
console.log(arr); // [1, 2, 3, 4]
```

</aside>

### **📌 35.2.2 splice**

<aside>
🔅

→ ES5에서 어떤 배열의 중간에 다른 배열의 요소들을 추가하거나 제거하려면 splice 메서드를 사용한다.

- 이때 splice 메서드의 세 번째 인수로 배열을 전달하면 배열 자체가 추가된다.

```jsx
// ES5
var arr1 = [1, 4];
var arr2 = [2, 3];

// 세 번째 인수 arr2를 해체하여 전달해야 한다.
// 그렇지 않으면 arr1에 arr2 배열 자체가 추가된다.
arr1.splice(1, 0, arr2);

// 기대한 결과는 [1, [2, 3], 4]가 아니라 [1, 2, 3, 4]다.
console.log(arr1); // [1, [2, 3], 4]
```

→ 위처럼 기대한 결과를 만들기 위해서는, apply 메서드를 사용하여 splice 메서드를 호출해야 한다.

```jsx
// ES5
var arr1 = [1, 4];
var arr2 = [2, 3];

// 원하는 결과를 만들어보자
Array.prototype.splice.apply(arr1, [1, 0].concat(arr2));
console.log(arr1); // [1, 2, 3, 4]

// 스프레드 문법으로 해결하기
arr1.splice(1, 0, ...arr2);
console.log(arr1); // [1, 2, 3, 4]
```

</aside>

### **📌 35.2.3 배열 복사**

<aside>
🔅

→ ES5에서 배열을 복사하려면 slice 메서드를 사용한다.

```jsx
// ES5
var origin = [1, 2];
var copy = origin.slice();

console.log(copy); // [1, 2]
console.log(copy === origin); // false

// 스프레드 문법을 사용해보자.
// ES6
const origin = [1, 2];
const copy = [...origin];

console.log(copy); // [1, 2]
console.log(copy === origin); // false
```

</aside>

### **📌 35.2.4 이터러블을 배열로 반환**

<aside>
🔅

→ ES5에서 이터러블을 배열로 변환하려면 Function.prototype.apply 또는 [Function.prototype.call](http://Function.prototype.call) 메서드를 사용해서 slice 메서드를 호출해야 한다.

```jsx
// ES5
function sum() {
	// 이터러블이면서 유사 배열 객체인 argumnets를 배열로 변환
	var args = Array.prototype.slice.call(arguments);
	
	return args.reduce(function (pre, cur) {
		return pre + cur;
	}, 0);
}

console.log(sum(1, 2, 3)); // 6

// 이터러블이 아닌 유사 배열 객체
const arrayLike = {
	0: 1,
	1: 2,
	2: 3,
	length: 3
};

const arr = Array.prototype.slice.call(arrayLike); // -> [1, 2, 3]
console.log(Array.isArray(arr)); // true

// 스프레드 문법을 사용하면 좀 더 간편하게 이터러블을 배열로 변환할 수 있다.
function sum() {
	// 이터러블이면서 유사 배열 객체인 arguments를 배열로 변환
	return [...arguments].reduce((pre, cur) => pre + cur, 0);
}
console.log(sum(1, 2, 3)); // 6

// Rest 파라미터로 사용도 가능하다.
// Rest 파라미터 args는 함수에 전달된 인수들의 목록을 배열로 전달받는다.
const sum = (..args) => args.reduce((pre, cur) => pre + cur, 0);
console.log(sum(1, 2, 3)); // 6

// 단 이터러블이 아닌 유사 배열 객체는 스프레드 문법의 대상이 될 수 없다.
// 이터러블이 아닌 유사 배열 객체
const arrayLike = {
	0: 1,
	1: 2,
	2: 3,
	length: 3
};

const arr = [...arrayLike];
// TypeError: object is not iterable
```

→ 이터러블이 아닌 유사 배열 객체를 배열로 변경하려면 ES6에서 도입된 Array.from 메서드를 사용한다.

```jsx
// Array.from은 유사 배열 객체 또는 이터러블을 배열로 변환한다.
Array.from(arrayLike); // -> [1, 2, 3]
```

</aside>

### ⭐️35.3 객체 리터럴 내부에서 사용하는 경우

<aside>
🔅

→ 스프레드 문법의 대상은 이터러블이어야하지만 스프레드 프로퍼티 제안은 일반 객체를 대상으로도 스프레드 문법의 사용을 허용한다.

```jsx
// 스프레드 프로퍼티
// 객체 복사(얕은 복사)
const obj = { x: 1, y: 2 };
const copy = { ...obj };
console.log(copy); // { x: 1, y: 2 }
console.log(obj === copy); // false

// 객체 병합
const merged = { x: 1, y: 2, ...{ a: 3, b: 4 } };
console.log(merged); // { x: 1, y: 2, a: 3, b: 4 }

// 스프에드 프로퍼티가 제안되기 이전 ES6에서 도입된 assign 메서드를 사용한다.
// 객체 병합. 프로퍼티가 중복되는 경우 뒤에 위치한 프로퍼티가 우선권을 갖는다.
const merged = Object.assign({}, {x: 1, y: 2}, { y: 10, z: 3 });
console.log(merged); // { x: 1, y: 10, z: 3 }

// 특정프로퍼티 변경
const changed = Object.assign({}, { x: 1, y: 2 }, { y: 100 });
console.log(changed); // { x: 1, y: 100 }

// 프로퍼티 추가
const added = Object.assign({}, { x: 1, y: 2 }, { z: 0 });
console.log(added); // { x:1, y:2, z: 0 }
```

→ 스프레드 프로퍼티는 Object.assign 메서드를 대체할 수 있는 간편한 문법이다.

```jsx
// 객체 병합. 프로퍼티가 중복되는 경우 뒤에 위치한 프로퍼티가 우선권을 갖는다.
const merged = { ...{ x: 1, y: 2 }, ...{ y: 10, z: 3 } };
console.log(merged); // { x: 1, y: 10, z: 3 }

// 특정 프로퍼티 변경
const changed = { ... { x: 1, y: 2 }, y: 100 };
console.log(changed); // { x: 1, y: 100 }

// 프로퍼티 추가
const added = { ... { x: 1, y: 2 }, z: 0 };
console.log(added); // { x : 1, y: 2, z: 0 }
```

</aside>