### ⭐️18.1 일급 객체

<aside>
🍕

→ 다음과 같은 조건을 만족하는 객체를 일급 객체라고 한다.

1. 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
3. 함수의 매개변수에 전달할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.

→ 자바스크립트 함수는 다음 예제와 같이 위의 조건을 모두 만족하므로 일급 객체다.

```jsx
// 1. 함수는 무명의 리터럴로 생성할 수 있다.
// 2. 함수는 변우세 저장할 수 있다.
// 런타임(할당 단계)에 함수 리터럴이 평가되어 함수 객체가 생성되고 변수에 할당된다.
const increase = function (num) {
	return ++num;
};

const decrease = function (num) {
	return --num;
};

// 2. 함수는 객체에 저장할 수 있다.
const predicates = { increase, decrease };

// 3. 함수의 매개변수에 전달할 수 있다.
// 4. 함수의 반환값으로 사용할 수 있다.
function makeCounter(predicate) {
	let num = 0;
	
	return function () {
		num = predicate(num);
		return num;
	};
}

// 3. 함수는 매개변수에게 함수를 전달할 수 있다.
const increaser = makeCounter(predicates.increase);
console.log(increaser()); // 1
console.log(increaser()); // 2

// 3. 함수는 매개변수에게 함수를 전달할 수 있다.
const decreaser = makeCounter(perdicates.decrease);
console.log(decreaser()); // -1
console.log(decreaser()); // -2
```

→ 함수는 곧 객체이다.

- 함수를 객체와 동일하게 사용할 수 있다.
- 객체는 값이므로 함수는 값과 동일하게 취급할 수 있다.
- 함수는 값을 사용할 수 있는 곳이라면 어디서든지 리터럴로 정의가 가능하며 런타임에 함수 객체로 평가된다.

→ 함수는 객체이지만 일반 객체와는 차이가 있다.

- 일반 객체는 호출할 수 없지만 함수 객체는 호출할 수 있다.
- 함수 객체는 일반 객체에는 없는 함수 고유의 프로퍼티를 소유한다.
</aside>

### ⭐️18.2 함수 객체의 프로퍼티

<aside>
⏰

→ 함수는 객체다.

- 함수도 프로퍼티를 가질 수 있다.

```jsx
function square (number) {
	return number * number;
}

console.dir(square);
```

![18-1.png](attachment:04280407-bb11-4717-8a33-c91b1eae0328:18-1.png)

→ square 함수의 모든 프로퍼티의 어트리뷰트를 Object.getOwnPropertyDescriptors 메서드로 확인 해보기

```jsx
function square (number) {
	return number * number;
}

console.log(Object.getOwnPropertyDescriptors(square));
/*
length: { value: 1, writable: false, enumerable: false, configurable: true },
name: { value: "square", writable: false, enumerable: false, configurable: true}
arguments:{value: null, writable: false, enumerable: false, configurable: false}
caller: { value: null, writable: false, enumerable: false, configurable: true}
prototype:{value: {...}, writable: true, enumerable: false, configurable: true}
*/

// __proto__ 는 square 함수의 프로퍼티가 아니다.
console.log(Object.getOwnPropertyDescriptor(square, '__proto__')); // undefined

// __proto__는 Object.prototype 객체의 접근자 프로퍼티다.
// square 함수는 Object.prototype 객체로부터 __proto__ 접근자 프로퍼티를 상속받는다
console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
// {get: f, set: f, enumerable: false, configurable: true}
```

→ 함수 프로퍼티와 일반 객체 프로퍼티의 차이

- arguments, caller, length, name, prototype 프로퍼티는 모두 함수 객체의 데이터 프로퍼티다.
- 일반 객체에는 없는 함수 객체 고유의 프로퍼티다.
- __proto__는 접근자 프로퍼티이며, 함수 객체 고유의 프로퍼티가 아닌, Object.prototype 객체의 프로퍼티를 상속받은 것이다.
- __proto__ 접근자 프로퍼티는 모든 객체가 상속받아 사용할 수 있다.
</aside>

### **📌 18.2.1 arguments 프로퍼티**

<aside>
❣️

→ 함수 객체의 arguments 프로퍼티 값은 arguments 객체다.

- arguments 객체는 함수 호출 시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체이며, 함수 내부에서 지역 변수처럼 사용된다.
- 함수 외부에서는 참조할 수 없다.
- 함수 내부에서 지역 변수처럼 사용할 수 있는 arguments 객체를 참조하도록 한다.

→ 자바스크립트는 함수의 매개변수와 인수의 개수가 일치하는지 확인하지 않는다.

- 함수 호출 시 매개변수 개수만큼 인수를 전달하지 않아도 에러가 발생하지 않는다.

```jsx
function multiply(x, y) {
	console.log(arguments);
	return x * y;
}

console.log(multiply()); // NaN
console.log(multiply(1)); // NaN
console.log(multiply(1, 2)); // 2
console.log(multiply(1, 2, 3)); // 2
```

→ 함수를 정의할 때 선언한 매개변수는 함수 몸체 내부에서 변수와 동일하게 취급된다.

- 함수가 호출되면 함수 몸체 내에서 암묵적으로 매개변수가 선언되고 undefined 초기화된 이후 인수가 할당된다.
- 선언된 매개변수의 개수보다 인수를 적게 전달했을 경우(multiply(), multiply(1)) 인수가 전달되지 않은 매개변수는 undefined로 초기화된 상태를 유지한다.
- 매개변수의 개수보다 인수를 더 많이 전달한 경우 (multiply(1,2,3)) 초과된 인수는 무시된다.
- 그렇다고 초과된 인수가 그냥 버려지진 않는다. 브라우저 콘솔로 확인해보기

![18-2.png](attachment:4e3c911c-fb72-44f0-be99-9069ee2347a9:18-2.png)

→ arguments 객체는 인수를 프로퍼티 값으로 소유하며 프로퍼티 키는 인수의 순서를 나타낸다.

- arguments 객체의 callee 프로퍼티는 호출되어 arguments 객체를 생성한 함수, 즉 함수 자신을 가리키고 arguments 객체의 length 프로퍼티는 인수의 개수를 가리킨다.
- 선언된 매개변수의 개수와 함수를 호출할 때 전달하는 인수의 개수를 확인하지 않는 자바스크립트의 특성 때문에 함수가 호출되면 인수 개수를 확인하고 이에 따라 함수의 동작을 달리 정의할 필요가 있다.
- 이때 유용하게 사용하는 것이 arguments 객체다.
- arguments 객체는 매개변수 개수를 확정할 수 없는 **가변 인자 함수**를 구현할 때 유용하다.

```jsx
function sum() {
	let res = 0;
	
	// arguments 객체는 length 프로퍼티가 있는 유사 배열 객체이므로 for문으로 순회
	for(let i = 0; i < arguments.length; i++) {
		res += arguments[i];
	}
	
	return res;
}

console.log(sum()); // 0
console.log(sum(1, 2)); // 3
console.log(sum(1, 2, 3)); // 6
```

→ arguments 객체는 배열 형태로 인자 정보를 담고 있지만 실제 배열이 아닌 유사 배열 객체다.

- 유사 배열 객체란 length 프로퍼티를 가진 객체로 for 문으로 순회할 수 있는 객체를 말한다.
- 유사 배열 객체는 배열이 아니므로 배열 메서드를 사용할 경우 에러가 발생한다.

```jsx
function sum() {
	// arguments 객체를 배열로 변환
	const array = Array.prototype.slice.call(arguments);
	return array.reduce(function (pre, cur) {
		return pre + cur;
	}, 0);
}

console.log(sum(1, 2)); // 3
console.log(sum(1, 2, 3, 4, 5)); // 15

// 이러한 번거로움을 해결하기 위해 ES6에서는 Rest 파라미터를 도입
// ES6 Rest parameter
function sum (...args) {
	return args.reduce((pre, cur) => pre + cur, 0);
}

console.log(sum(1, 2)); // 3
console.log(sum(1, 2, 3, 4, 5)); // 15
```

→ ES6 Rest 파라미터의 도입으로 arguments 객체의 중요성이 이전 같지는 않다 ㅠㅠ

</aside>

### **📌 18.2.2 caller 프로퍼티**

<aside>
💯

→ caller 프로퍼티는 ECMAScript 사양에 포함되지 않은 비표준 프로퍼티다.

- 표준화될 예정도 없는 프로퍼티이므로 사용하지 말고 참고로만 알아두자.
- 함수 객체의 caller 프로퍼티는 함수 자신을 호출한 함수를 가리킨다.

```jsx
function foo(func) {
	return func();
}

function bar() {
	return 'caller : ' + bar.caller;
}

// 브라우저에서의 실행한 결과
console.log(foo(bar)); // caller : function foo(func) {...}
console.log(bar()); // caller : null
```

→ 함수 호출 foo(bar)의 경우 bar 함수를 foo 함수 내에서 호출했다. 

- 이때 bar 함수의 caller 프로퍼티는 bar 함수를 호출한 foo 함수를 가리킨다.
- 함수 호출 bar()의 경우 bar 함수를 호출한 함수는 없다.
- 따라서 caller 프로퍼티는 null을 가리킨다.
</aside>

### **📌 18.2.3 length 프로퍼티**

<aside>
💥

→ 함수 객체의 length 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킨다.

```jsx
function foo() {}
console.log(foo.length); // 0

function bar(x) {
	return x;
}
console.log(bar.length); // 1

function baz(x, y) {
	return x * y;
}

console.log(baz.length); // 2
```

→ argumnets 객체의 length 프로퍼티와 함수 객체의 length 프로퍼티의 값은 다를 수 있으므로 주의해야 한다.

- argumnets 객체의 length 프로퍼티는 인자의 개수를 가리키고, 함수 객체의 length 프로퍼티는 매개변수의 개수를 가리킨다.
</aside>

### **📌 18.2.4 name 프로퍼티**

<aside>
🍡

→ 함수 객체의 name 프로퍼티는 함수 이름을 나타낸다.

- name 프로퍼티는 ES6 이전까지는 비표준이었다가 ES6에서 정식 표준이 되었다.
- name 프로퍼티는 ES5와 ES6에서 동작을 달리하므로 주의해야 한다.
- 익명 함수 표현식의 경우 ES5에서 name프로퍼티는 빈 문자열을 값을 갖는다.
- ES6에서는 함수 객체를 가리키는 식별자를 값으로 갖는다.

```jsx
// 기명 함수 표현식
var namedFunc = function foo() {}; 
console.log(namedFunc.name); // foo

// 익명 함수 표현식
var annoymousFunc = function () {};
// ES5: name 프로퍼티는 빈 문자열을 값으로 갖는다.
// ES6: name 프로퍼티는 함수 객체를 가리키는 변수 이름을 값으로 갖는다.
console.log(anonymousFunc.name); // anonymousFunc

// 함수 선언(Function declaration)
function bar() {}
console.log(bar.name); // bar
```

</aside>

### **📌 18.2.5 __proto__ 접근자 프로퍼티**

<aside>
🍴

→ 모든 객체는 [[Prototype]] 이라는 내부 슬롯을 갖는다.

- [[Prototype]] 내부 슬롯은 객체지향 프로그래밍의 상속을 구현하는 프로토 타입 객체다.
- __proto__ 프로퍼티는 [[Prototype]] 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티 이다.
- 내부 슬롯에는 직접 접근할 수 없고 간접적인 접근 방법을 제공하는 경우에 한하여 접근할 수 있다.
- [[Prototype]] 내부슬롯에도 직접 접근할 수 없으며 __proto__ 접근자 프로퍼티를 통해 간접적으로 프로토타입 객체에 접근할 수 있다.

```jsx
const obj = { a: 1 };

// 객체 리터럴 방식으로 생성한 객체의 프로토타입 객체는 Object.prototype이다.
console.log(obj.__proto__ === Object.prototype); // true

// 객체 리터럴 방식으로 생성한 객체는 프로토타입 객체인 Object.prototype의 
// 프로퍼티를 상속 받는다.
// hasOwnProperty 메서드는 Object.prototype의 메서드다.
console.log(obj.hasOwnProperty('a')); // true
console.log(obj.hasOwnProperty('__proto__')); // fasle
```

</aside>

### **📌 18.2.6 prototype 프로퍼티**

<aside>
🦹

→ prototype 프로퍼티는 생성자 함수로 호출할 수 있는 함수 객체

- constructor만이 소유하는 프로퍼티다.
- 일반 객체와 생성자 함수로 호출할 수 없는 non-constructor에는 prototype 프로퍼티가 없다.

```jsx
// 함수 객체는 prototype 프로퍼티를 소유한다.
(function () {}).hasOwnProperty('prototype'); // true

// 일반 객체는 prototype 프로퍼티를 소유하지 않는다.
({}).hasOwnProperty('prototype'); // false
```

</aside>