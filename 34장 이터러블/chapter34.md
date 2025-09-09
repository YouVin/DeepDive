### ⭐️34.1 이터레이션 프로토콜

<aside>
🔅

→ ES6에서 도입된 이터레이션 프로토콜은 순회 가능한 데이터 컬렉션을 만들기 위해 ECMAScript 사양에 정의하여 미리 약속한 규칙이다.

- ES6 이전의 순회 가능한 데이터 컬렉션, 즉 배열, 문자열, 유사배열 객체, DOM 컬렉션를 규칙없이 나름의 구조로 순회할 수 있었다.
- ES6에서는 순회 가능한 데이터 컬렉션을 이터레이션 프로토콜을 준수하는 이터러블로 통일하여 for…of 문, 스프레드 문, 배열 디스트럭처링 할당의 대상으로 사용할 수 있도록 일원화 했다.
- 이터레이션 프로토콜에는 이터러블 프로토콜과 이터레이터 프로토콜이 있다.
1. 이터러블 프로토콜
    1. Symbol.iterator를 프로퍼티 키로 사용한 메서드를 구현하거나 포로토타입 체인을 통해 상속 받은 Symbol.iterator 메서드를 호출하면 프로토콜을 준수한 이터레이터를 반환한다.
    2. 이러한 규약을 이터러블 프로토콜이라 하며, 이터러블 프로토콜을 준수한 객체를 이터러블이라 한다.
    3. 이터러블은 for…of 문으로 순회할 수 있으며 스프레드 문법과 배열 디스트럭처링 할당의 대상으로 사용할 수 있다.
2. 이터레이터 프로토콜
    1. 이터러블의 Symbol.iterator 메서드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터를 반환한다.
    2. 이터레이터는 next메서드를 소유하며 next 메서드를 호출하면 이터러블을 순회하며 value과 done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환한다.
    3. 이러한 규약을 이터레이터 프로토콜이라 하며, 이터레이터 프로토콜을 준수한 객체를 이터레이터라 한다.
</aside>

### **📌 34.1.1 이터러블**

<aside>
🔅

→ 이러터블 프로토콜을 준수한 객체를 이터러블이라 한다.

- 이터러블은 Symbol.iterator를 프로퍼티 키로 사용한 메서드를 직접 구현하거나 프로토타입 체인을 통해 상속받은 객체를 말한다.

```jsx
const isIterable = v => v !== null && typeof v[Symbol.iterator] === 'function';

// 배열 문자열 Map Set 등은 이터러블이다.
isIterable([]);  // -> true
isIterable(''); // -> true
isIterable(new Map()); // -> true
isIterable(new Ser()); // -> true
isIterable({}); // -> false

// 이터러블은 for...of 문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링
// 할당의 대상으로 사용할 수 있다.
const array = [1, 2, 3];

// 배열은 Array.prototype의 Symbol.iterator 메서드를 상속받는 이터러블이다.
console.log(Symbol.iterator in array); // true
// 이터러블 배열은 for...of 문으로 순회 가능하다.
for (const item of array) {
	console.log(item);
}
// 이터러블인 배열은 스프레드 문법의 대상으로 사용할 수 있다.
console.log([...array]); // [1, 2, 3]
// 이터러블인 배열은 배열 디스트럭처링 할당의 대상으로 사용할 수 있다.
const [a, ...rest] = array;
console.log(a, rest); // 1, [2, 3]

// 메서드를 직접 구현하지 않거나 상속받지 않은 일반 객체는 이터러블 프로토콜을 
// 준수한 이터러블이 아니다. 따라서 일반 객체는 for...of 문으로 순회할 수 없다.
const obj = { a: 1, b: 2};

// 일반 객체는 메서드로 구현한게 아니라 이터러블 프로토콜이 아니다.
console.log(Symbol.iterator in obj); // false
// 이터러블이 아닌 일반 객체는 for...of 문으로 순회할 수 없다.
for(const item of obj) {
	console.log(item);
}

// 이터러블이 아닌 일반 객체는 배열 디스트럭처링 할당의 대상으로 사용할 수 없다.
const [a, b] = obj; // -> Type Error
```

</aside>

### **📌 34.1.2 이터레이터**

<aside>
🔅

→ 이터러블의 Symbol.iterator 메서드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터를 반환한다.

- 이터러블의 Symbol.iterator 메서드가 반환한 이터레이터는 next 메서드를 갖는다.

```jsx
// 배열은 이터러블 프로토콜을 준수한 이터러블이다.
const array = [1, 2, 3];

// Symbol.iterator 메서드는 이터레이터를 반환한다.
const iterator = array[Symbol.iterator]();

// Symbol.iterator 메서드가 반환한 이터레이터는 next 메서드를 갖는다.
console.log('next' in iterator); // true

// next 메서드를 호출하면 이터러블을 순회하며 순회 결과를 나타내는 이터레이터
// 리절트 객체를 반환한다. 객체니는 value 와 done 을 갖는다.
console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value 2, done: false }
```

</aside>

### ⭐️34.2 빌트인 이터러블

<aside>
🔅

→ 자바스크립트는 이터레이션 프로토콜을 준수한 객체인 빌트인 이터러블을 제공한다.

| 빌트인 이터러블 | Symbol.iterator 메서드 |
| --- | --- |
| Array | Array.prototype[Symbol.iterator] |
| String | String.prototype.[Symbol.iterator] |
| Map | Map.prototype[Symbol.iterator] |
| Set | Set.prototype[Symbol.iterator] |
| TypedArray | TypedArray.prototype[Symbol.iterator] |
| arguments | arguments[Symbol.iterator] |
</aside>

### ⭐️34.3 for…of 문

<aside>
🔅

→ for…of 문은 이터러블을 순회하면서 이터러블의 요소를 변수에 할당한다.

for ( 변수 선언문 of 이터러블 ) { … }

//  for…of 문은 for…in 문의 형식과 매우 유사하다.

for ( 변수 선언문 in 객체 ) { … }

→ for…of 문은 내부적으로 이터레이터의 next 메서드를 호출하여 이터러블을 순회하며 next 메서드가 반환한 이터레이터 리절트 객체의 value 프로퍼티 값을 for…of 문의 변수에 할당한다.

```jsx
for ( const item of [1, 2, 3]) {
	// item 변수에 순차적으로 1, 2, 3이 할당된다.
	console.log(item); // 1 2 3
}

// 이를 for 문으로 보여주면?
// 이터러블
const iterable = [1 ,2, 3];
// 이터러블의 Symbol.iterator 메서드를 호출하여 이터레이터를 생성한다.
const iterator = iterable[Symbole.iterator]();
for (;;) {
	// 이터레이터 next 메서드를 호출하여 이터러블을 순회한다.
	// 이때 next 메서드는 이터레이터 리절트 객체를 반환한다.
	const res = iterator.next();
	// next 메서드가 반환한 이터레이터 리절트 객체의 done 프로퍼티 값이 true
	// 이면 순회를 중단한다.
	if(res.done) break;
	// 이터레이터 리절트 객체의  value 프로퍼티 값을 item 변수에 할당한다.
	const item = res.value;
	console.log(item); // 1 2 3
}
```

</aside>

### ⭐️34.4 이터러블과 유사 배열 객체

<aside>
🔅

→ 유사 배열 객체는 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체를 말한다.

- 유사 배열 객체는 length 프로퍼티를 갖기 때문에 for 문으로 순회할 수 있고, 인덱스를 나타내는 숫자 형식의 문자열을 프로퍼티 키로 가지므로 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있다.

```jsx
// 유사 배열 객체
const arrayLike = {
	0: 1,
	1: 2,
	2: 3,
	length: 3
};

// 유사 배열 객체는 length 프로퍼티를 갖기 때문에 for 문으로 순회할 수 있다.
for( let i = 0; i < arrayLike.length; i++) {
	// 유사 배열 객체는 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있다.
	console.log(arrayLike[i]); // 1 2 3
}

// 유사 배열 객체는 이터러블이 아니기 때문에 for...of 문으로 순회할 수 없다.
for( const item of arrayLike) {
	console.log(item); // 1 2 3
}
// -> TypeError

// Array.from은 유사 배열 객체 또는 이터러블을 배열로 반환한다.
const arr = Array.from(arrayLike);
console.log(arr); // [1, 2, 3]
```

</aside>

### ⭐️34.5 이터레이션 프로토콜의 필요성

<aside>
🔅

→ 이터러블은 for…of 문, 스프레드 문법, 배열 디스트럭처링 할당과 같은 데이터 소비자에 의해 사용되므로 데이터 공급자의 역할을 한다고 할 수 있다.

- 데이터 공급자가 각자의 순회 방식을 갖는다면 데이터 소비자는 다양한 데이터 공급자의 순회 방식을 모두 지원해야 한다.

### 상황을 비유로 설명

- **데이터 공급자(이터러블)** = “책장에 꽂힌 책들”
- **데이터 소비자(for…of, 스프레드, 디스트럭처링 등)** = “책을 읽는 사람들”

만약 **책장이 제각각 자기만의 규칙**(예: 한 칸은 위에서 아래로 읽어야 하고, 다른 칸은 오른쪽에서 왼쪽으로 읽어야 함)을 갖고 있다면?

책을 읽는 사람은 책장마다 다른 규칙을 다 외워야 하고, 그에 맞춰 읽는 방법을 매번 바꿔야 해. 

→ 이건 너무 비효율적

### 그래서 나온 게 **이터레이션 프로토콜**

자바스크립트는 **모든 책장은 이 규칙만 따르면 돼!**라는 공통 인터페이스를 만들어줬어.

그게 바로 이터레이션 프로토콜(Iterator Protocol)

규칙은 간단하다.

1. `Symbol.iterator` 메서드를 가지고 있어야 함
2. 그 안에서 `next()`를 호출했을 때 `{ value, done }` 객체를 반환해야 함

이렇게만 지키면,

- `for…of`
- 스프레드(`...`)
- 배열/객체 디스트럭처링

같은 **소비자**들이 일관되게 쓸 수 있어.

### 핵심 정리

- **이터러블 = 공급자** → 데이터를 어떤 순서로 내줄지 정하는 쪽
- **이터레이터 프로토콜 = 약속된 규칙** → 공급자가 일관되게 데이터를 줄 수 있게 하는 장치
- 데이터 소비자(for…of, … 등)는 → “규칙이 통일되어 있으니, 따로 공부 안 하고도 모든 공급자한테서 데이터를 똑같이 받을 수 있음”
</aside>

### ⭐️34.6 사용자 정의 이터러블

### **📌 34.6.1 사용자 정의 이터러블 구현**

<aside>
🔅

→ 이터레이션 프로토콜을 준수하지 않는 일반 객체도 이터레이션 프로토콜을 준수하도록 구현하면 사용자 정의 이터러블이 된다.

```jsx
// 파보나치 수열을 구현한 사용자 정의 이터러블
const fibonacci = {
	// Symbol.iterator 메서드를 구현하여 이터러블 프로토콜을 준수한다.
	[Symbol.iterator]() {
		let [pre, cur] = [0, 1]; 
		const max = 10; // 수열의 최대값
		
		// Symbol.iterator 메서드는 next 메서드를 소유한 이터레이터를 반환
		// next 메서드는 이터레이터 리절트 객체를 반환해야 한다.
		return {
			next() {
				[pre, cur] = [cur, pre + cur]; 
				// 이터레이터 리절트 객체를 반환한다.
				return { value: cur, done: cur >= max };
			}
		};
	}
};

// 이터러블인 fibonacci 객체를 순회할 때마다 next 메서드가 호출된다.
for (const num of fibonacci) {
	console.log(num); // 1 2 3 5 8
}

// 사용자 정의 이터러블은 이터레이션 프로토콜을 주수하도록 메서드를 구현하고
// next 메서드를 갖는 이터레이터를 반환하도록 한다.
// 이터러블은 스프레드 문법의 대상이 될 수 있다.
const arr = [...fibonacci];
console.log(arr); // [1, 2, 3, 5, 8]

// 이터러블은 배열 디스트럭처링 할당의 대상이 될 수 있다.
const [first, second, ...rest] = fibonacci;
console.log(first, second, rest); // 1 2 [3, 5, 8]
```

</aside>

### **📌 34.6.2 이터러블을 생성하는 함수**

<aside>
🔅

→ 앞에서 살펴본 fibonacci 이터러블은 내부에 수열의 최대값 max를 가지고 있다.

- 수열의 최대값은 고정된 값으로 외부에서 전달한 값으로 변경할 방법이 없다는 아쉬움이 있다.
- 수열의 최대값을 외부에서 전달할 수 있도록 수정해 보자.

```jsx
// 피보나치 수열을 구현한 사용자 정의 이터러블을 반환하는 함수
// 수열의 최대값을 인수로 전달받는다.
const fibonacciFunc = function (max) {
	let [pre, cur] = [0, 1];
	
	// Symbol.iterator 메서드를 구현한 이터러블을 반환한다.
	return {
		[Symbol.iterator]() {
			return {
				next() {
					[pre, cur] = [cur, pre + cur];
					return { value: cur, done: cur >= max };
				}
			};
		}
	};
};

// 이터러블을 반환하느 함수에 수열의 최대값을 인수로 전달하면서 호출한다.
// fibonacciFunc(10)은 이터러블을 반환한다
for(const num of fibonacciFunc(10)) {
	console.log(num); // 1 2 3 5 8
}
```

</aside>

### **📌 34.6.3 이터러블이면서 이터레이터인 객체를 생성하는 함수**

<aside>
🔅

→ fibonacciFunc 함수는 이터러블을 반환한다.

- 만약 이터레이터를 생성하려면 이터러블의 Symbol.iterator 메서드를 호출해야 한다.

```jsx
// fibonacciFunc 함수는 이터러블을 반환한다.
const iterable = fibonacciFunc(5);
// 이터러블의 Symbol.iterator 메서드는 이터레이터를 반환한다.
const iterator = iterable[Symbol.iterator]();

console.log(iterator.next()); // { value : 1, done: false }
console.log(iterator.next()); // { value : 2, done: false }
console.log(iterator.next()); // { value : 3, done: false }
console.log(iterator.next()); // { value : 5, done: true }
```

→ 이터러블이면서 이터레이터인 객체로 반환하려면?

```jsx
// 이터러블이면서 이터레이터인 객체.
// 이터레이터를 반환 Symbol.iterator 메서드로 리절트 객체를 반환
{ 
	[Symbol.iterator]() { return this; },
	next() {
		return { value: any, done: boolean };
	}
}

// 이터러블이면서 이터레이터인 객체를 반환하는 함수 -> 피보나치 함수
const fibonacciFunc = function (max) { 
	let [pre, cur] = [0, 1];
	
	// Symbol.iterator 메서드와 next 메서드를 소유한 이터러블이면서 이터레이터인
	// 객체를 반환
	return {
		[Symbol.iterator]() { reutn this; },
		// next 메서드는 이터레이터 리절트 객체를 반환
		next() {
			[pre, cur] = [cur, pre + cur];
			return { value: cur, done: cur >= max };
		}
	};
};

// iter는 이터러블 이면서 이터레이터다.
let iter = fibonacciFunc(10);

// iter는 이터러블 이므로 for..of 문을 순회할 수 있다.
for (const num of iter) {
	console.log(num); // 1 2 3 5 8
}

// iter는 이터러블이면서 이터레이터다.
iter = fibonacciFunc(10);

// iter는 이터레이터 므로 리절트 객체를 반환한다.
console.log(iterator.next()); // { value : 1, done: false }
console.log(iterator.next()); // { value : 2, done: false }
console.log(iterator.next()); // { value : 3, done: false }
console.log(iterator.next()); // { value : 5, done: false }
console.log(iterator.next()); // { value : 8, done: false }
console.log(iterator.next()); // { value : 13, done: true}
```

</aside>

### **📌 34.6.4 무한 이터러블과 지연 평가**

<aside>
🔅

→ 무한 이터러블을 생성하는 함수를 정의해보자. 이를 통해 무한 수열을 간단하게 구현할 수 있다.

```jsx
// 무한 이터러블을 생성하는 함수
const fibonacciFunc = function () { 
	let [pre, cur] = [0, 1];
	
	// Symbol.iterator 메서드와 next 메서드를 소유한 이터러블이면서 이터레이터인
	// 객체를 반환
	return {
		[Symbol.iterator]() { reutn this; },
		// next 메서드는 이터레이터 리절트 객체를 반환
		next() {
			[pre, cur] = [cur, pre + cur];
			// 무한 생성을 위한 done 프로퍼티를 생략한다.
			return { value: cur };
		}
	};
};

// fibonacciFunc는 무한 이터러블을 생성한다.
for (const num of fibonacciFunc()) {
	if(num > 10000); break;
	console.log(num);  // 1 2 3 5 8... 6765
}

// 배열 디스트럭처링 할당을 통해 무한 이터러블에서 3개의 요소만 취득한다.
const [f1, f2, f3] = fibonacciFunc();
console.log(f1, f2, f3); // 1 2 3
```

</aside>