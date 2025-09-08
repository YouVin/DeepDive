### ⭐️33.1 심벌이란?

<aside>
🔅

→ 1997년 자바스크립트가 ECMAScript로 표준화된 이래로 자바스크립트에는 6개의 타입

문자열, 숫자, 불리언, undefined, null, 객체 타입이 있었다.

- 심벌은 ES6에서 도입된 7번째 데이터 타입으로 변경 불가능한 원시 타입의 값이다.
- 심벌 값은 다른 값과 중복되지 않는 유일무이한 값이다.
- 이름의 충돌 위험이 없는 유일한 프로퍼티 키를 만들기 위해 사용한다.
</aside>

### ⭐️33.2 심벌 값의 생성

### **📌 33.2.1 Symbol 함수**

<aside>
🔅

→ 심벌 값은 Symbol 함수를 호출하여 생성한다.

- 다른 타입의 값은 리터럴 표기법을 통해 값을 생성할 수 있었지만, 심벌 값은 Symbol 함수를 호출하여 생성해야 한다.
- 다른 값과 절대 중복되지 않는 유일무이한 값이다.

```jsx
// Symbol 함수를 호출하여 유일무이한 심벌 값을 생성한다.
const mySymbol = Symbol();
console.log(typeof mySymbol); // symbole

// 심벌 값은 외부로 노출되지 않아 확인할 수 없다.
console.log(mySymbol); // Symbol()

// new 연산자와 함께 호출하지 않는다.
// new와 호출 시 객체가 생성되지만 심벌 값은 변경 불가능한 원시 값이다.
new Symbol(); // TypeError

// 심벌 값에 대한 설명이 같더라도 유일무이한 심벌 값을 생성한다.
const mySymbol1 = Symbol("mySymbol");
const mySymbol2 = Symbol("mySymbol");
console.log(mySymbol1 === mySymbol2); // false

// 심벌 값도 문자열, 숫자 불리언과 같이 객체처럼 접근 시 래퍼 객체를 생성한다.
console.log(mySymbol.description); // mySymbol
console.log(mySymbol.toString()); // Symbol(mySymbol)
```

→ 심벌 값의 타입 변환

```jsx
const mySymbol = Symbol();

// 심벌 값은 암묵적으로 문자열이나 숫자 타입으로 변환되지 않는다.
console.log(mySymbol + ''); // TypeError
console.log(+mySymbol); // TypeError

// 단 불리언 타입으로는 암묵적으로 타입 변환된다.
console.log(!!mySymbol); // true

// if 문 등에서 존재 확인이 가능하다.
if (mySymbol) console.log('mySymbol is not empty');
```

</aside>

### **📌 33.2.2 Symbol.for / Symbol.keyFor 메서드**

<aside>
🔅

→ Symbol.for 메서드는 인수로 전달받은 문자열을 키로 사용하여 키와 심벌 값의 쌍들이 저장되어 있는 전역 심벌 레지스트리에서 해당 키와 일치하는 심벌 값을 검색한다.

- 검색에 성공하면 새로운 심벌 값을 생성하지 않고 검색된 심벌 값을 반환한다.
- 검색에 실패하면 새로운 심벌 값을 생성하여 Symbol.for 메서드의 인수로 전달된 키로 전역 심벌 레지스트리에 저장한 후, 생성된 심벌 값을 반환한다.

```jsx
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 없으면 새로 생성
const s1 = Symbol.for('mySymbol');
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 있으면 해당 반환
const s2 = Symbol.for('mySymbol');

console.log(s1 === s2); // true
```

→ Symbol.keyfor 메서드를 사용하면 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출할 수 있다.

```jsx
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 없으면 새로 생성
const s1 = Symbol.for('mySymbol');
// 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출
Symbol.keyFor(s1); // -> mySymbol

// Symbol 함수를 호출하여 생성한 심벌 값은 전역 심벌 레지스트리에 등록 되어 관리x
const s2 = Symbol('foo');
// 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출
Symbol.keyFor(s2); // -> undefined
```

</aside>

### ⭐️33.3 심벌과 상수

<aside>
🔅

→ 예를 들어, 4방향 위, 아래, 왼쪽, 오른쪽을 나타내는 상수를 정의한다고 생각하자.

```jsx
// 위 아래 왼쪽 오른쪽을 나타내는 상수를 정의한다.
// 값 1, 2, 3, 4에는 특별한 의미가 없고 상수 이름에 의미가 있다.
const Direction = {
	UP: 1,
	DOWN: 2,
	LEFT: 3,
	RIGTH: 4
};

// 변수에 상수를 할당
const myDirection = Direction.UP;

if(myDirection === Direction.UP) {
	console.log('You are going UP.');
}
```

- 값에는 특별한 의미가 없고, 상수 이름 자체에 의미가 있는 경우가 있다.
- 문제는 상수 값 1, 2, 3, 4가 변경될 수 있으며, 다른 변수 값과 중복될 수 도 있다는 점이다.
- 이런 경우에 무의미한 상수 대신 중복될 가능성이 없는 유일무이한 심벌 값을 사용한다.

```jsx
// 위 아래 왼쪽 오른쪽을 나타내는 상수를 정의한다.
// 중복될 가능성이 없는 심벌 값으로 상수 값을 생성한다.
const Direction = {
	UP: Symbol('up'),
	DOWN: Symbol('down'),
	LEFT: Symbol('left'),
	RIGHT: Symbol('right')
};

const myDirection = Direction.UP;

if(myDirection === Direction.UP) {
	console.log('You are going UP.');
}
```

</aside>

### ⭐️33.4 심벌과 프로퍼티 키

<aside>
🔅

→ 객체의 프로퍼티 키는 빈 문자열을 포함하는 모든 문자열 또는 심벌 값으로 만들 수 있으며, 동적으로 생성할 수도 있다.

- 심벌 값으로 프로퍼티 키로 사용하려면 프로퍼티 키로 사용할 심벌 값에 대괄호를 사용해야 한다.
- 프로퍼티에 접근할 때도 마찬가지로 대괄호를 사용해야 한다.
- 심벌 값은 유일무이한 값이므로 심벌 값으로 프로퍼티 키를 만들면 다른 프로퍼티 키와 절대 충돌하지 않는다.

```jsx
const obj = {
	// 심벌 값으로 프로퍼티 키를 생성
	[Symbol.for('mySymbol')]: 1
};

obj[Symbol.for('mySymbole')]; // -> 1
```

</aside>

### ⭐️33.5 심벌과 프로퍼티 은닉

<aside>
🔅

→ 심벌 값을 프로퍼티 키로 사용하여 생성한 프로퍼티는 for…in 문이나 Object.keys, Object.getOwnPropertyNames 메서드로 찾을 수 없다.

- 심벌 값을 프로퍼티 키로 사용하여 프로퍼티를 생성하면 외부에 노출할 필요가 없는 프로퍼티를 은닉할 수 있다.

```jsx
const obj = {
	// 심벌 값으로 프로퍼티 키를 생성
	[Symbol('mySymbol')]: 1
};

for(const key in obj) {
	console.log(key); // 아무것도 출력되지 않는다.
}

console.log(Object.keys(obj)); // []
console.log(Object.getOwnPropertyNames(obj)); // []
```

→ 프로퍼티를 완전하게 숨길 수 있는 것은 아니다.

- ES6 에서 도입된 Object.getOwnPropertySymbols 메서드를 사용하면 심벌 값을 프로퍼티 키로 사용하여 생성한 프로퍼티를 찾을 수 있다.

```jsx
const obj = {
	// 심벌 값으로 프로퍼티 키를 생성
	[Symbol('mySymbol')]: 1
};

// getOwnPropertySymbols 메서드는 인수로 전달한 객체의 프로퍼티 키를 배열로 반환
console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(mySymbol)]

// getOwnPropertySymbols 메서드로 심벌 값도 찾을 수 있다.
const symbolkey1 = Object.getOwnPropertySymbols(obj)[0]; 
console.log(obj[symbolkey1]); // 1
```

</aside>

### ⭐️33.6 심벌과 표준 빌트인 객체 확장

<aside>
🔅

→ 일반적으로 표준 빌트인 객체에 사용자 정의 메서드를 직접 추가하여 확장하는 것은 권장하지 않는다.

- 표준 빌트인 객체는 읽기 전용으로 사용하는 것이 좋다.
- why? 개발자가 직접 추가한 메서드와 미래에 표준 사양으로 추가될 메서드의 이름과 중복이 될 가능성이 있기 때문에!

```jsx
// 표준 빌트인 객체를 확장하는 것은 권장하지 않는다.
Array.prototype.sum = function () {
	return this.reduce((acc, cur) => acc + cur, 0);
};

[1, 2].sum(); // -> 3

// 심벌 값으로 프로퍼티 키를 동적 생성하여 충돌하지 않도록 설정
Array.prototype[Symbol.for('sum')] = function () {
	return this.reduce((acc, cur) => acc + cur, 0);
};

[1, 2][Symbol.for('sum')](); // -> 3
```

</aside>

### ⭐️33.7 Well-known Symbol

<aside>
🔅

→ 자바스크립트가 기본 제공하는 빌트인 심벌 값이 있다.

- 빌트인 심벌 값은 Symbol 함수의 프로퍼티에 할당되어 있다.
- 기본 제공하는 빌트인 심벌 값을 ECMAScript 사양에서는 Well-known Symbol이라 부른다.

```jsx
// 1 ~ 5 범위의 정수로 이루어진 이터러블
const iterable = {
	// Symbol.iterable 메서드를 구현하여 이터러블 프로토콜을 준수
	[Symbol.iterator]() {
		let cur = 1;
		const max = 5;
		// Symbol.iterator 메서드는 next 메서드를 소유한 이터레이터를 반환
		return {
			next() {
				return { value: cur++, done: cur > max + 1 };
			}
		};
	}
};
for (const num of iterable) {
	console.log(num); // 1 2 3 4 5
}
```

</aside>