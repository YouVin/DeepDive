### ⭐️Object 생성자 함수

<aside>
🎴

→ new 연산자와 함께 Object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다. 

- 빈 객체를 생성한 이후 프로퍼티 또는 메서드를 추가하여 객체를 완성할 수 있다.

```jsx
// 빈객체의 생성
const person = new Object();

// 프로퍼티 추가
person.name = 'Lee';
person.sayHello = function () {
	console.log('Hi! My name is ' + this.name);
};

console.log(person); // {name: "Lee", sayHello: f}
person.sayHello(); // Hi! My name is Lee
```

→ 생성자 함수란 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수를 말한다.

- 생성자 함수에 의해 생성된 객체를 인스턴스라 한다.
- 자바스크립트는 Object 생성자 함수 이외에도 String, Number, Boolean, Function, Array, Date, RegExp, Promise 등의 빌트인 생성자 함수를 제공한다.

```jsx
// String 생성자 함수에 의한 String 객체 생성
const strObj = new String('Lee');
console.log(typeof strObj); // object
console.log(strObj); // String {"Lee"}

// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(123);
console.log(typeof numObj); // object
console.log(numObj); // Number {123}

// Boolean 생성자 함수에 의한 Boolean 객체 생성
const boolObj = new Boolean(true);
console.log(typeof boolObj); // object 
console.log(boolObj); // Boolean {true}

// Function 생성자 함수에 의한 Function 객체(함수) 생성
const func = new Function('x', 'return x * x');
console.log(typeof func); // function
console.dir(func); // f anonymous(x)

// Array 생성자 함수에 의한 Array 객체(배열) 생성
const arr = new Array(1,2,3);
console.log(typeof arr); // object
console.log(arr); // [1,2,3]

// RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성
const regExp = new RegExp(/ab+c/i);
console.log(typeof regExp); // object
console.log(regExp); // /ab+c/i

// Date 생성자 함수에 의한 Date 객체 생성
const date = new Date();
console.log(typeof date); // object 
console.log(date); // Mon May 04 2020 08:36:33 GMT+0900 (대한민국 표준시)
```

→ 반드시 Object 생성자 함수를 사용해 빈 객체를 생성해야 하는 것은 아니다.

- 객체를 생성하는 방법은 객체 리터럴을 사용하는 것이 더 간편하다.
- Object 생성자 함수를 사용해 객체를 생성하는 방식은 특별한 이유가 없다면 그다지 유용해 보이지 않는다.
</aside>

### ⭐️생성자 함수

### **📌 객체 리터럴에 의한 객체 생성 방식의 문제점**

<aside>
👑

→ 동일한 프로퍼를 갖는 객체를 여러 개 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야 하기 때문에 비효율적이다.

```jsx
const circle1 = {
	radius: 5,
	getDiameter() {
		return 2 * this.radius;
	}
};

console.log(circle1.getDiameter()); // 10

const circle2 = {
	getDiameter() { 
		return 2 * this.radius;
	}
};

console.log(circle2.getDiameter()); // 20
```

→ 객체는 프로퍼를 통해 객체 고유의 상태를 표현한다.

- 메서드를 통해 상태 데이터인 프로퍼티를 참조하고 조작하는 동작을 표현한다.
- 프로퍼티는 객체마다 프로퍼티 값이 다를 수 있지만 메서드는 내용이 동일한 경우가 일반적이다.
- 원을 표현한 원1객체, 원2 객체는 프로퍼티 구조가 동일하다.
- 객체 고유의 상태 데이터인 radius 프로퍼티 값은 객체마다 다르지만, getDiameter 메서드는 동일하다.
- But. 매번 같은 프로퍼티와 메서드를 기술?  지금이야 2개지만 많다면 …
</aside>

### **📌 생성자 함수에 의한 객체 생성 방식의 장점**

<aside>
🐆

→ 생성자 함수에 의한 객체 생성 방식은 마치 객체를 생성하기 위한 템플릿 처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.

```jsx
// 생성자 함수
function Circle(radius) {
	// 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
	this.radius = radius;
	this.getDiameter = function () {
		return 2 * this.radius;
	};
}

// 인스턴스의 생성
const circle1 = new Circle(5); // 반지름이 5인 Circle 객체 생성
const circle2 = new Circle(10); // 반지름이 10인 Circle 객체 생성

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20
```

<aside>
⚠️

→ this?

this는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수다.

this가 가리키는 값, 즉 thjis 바인딩은 함수 호출 방식에 따라 동적으로 결정된다.

| 함수 호출 방식 | this가 가리키는 값 |
| --- | --- |
| 일반 함수로서 호출 | 전역 객체 |
| 메서드로서 호출 | 메서드를 호출한 객체 |
| 생성자 함수로서 호출 | 생성자 함수가 생성할 인스턴스 |

```jsx
function foo() {
	console.log(this);
}

// 일반적인 함수로서 호출
// 전역 객체는 브라우저 환경에서는 window, Node.js 환경에서는 global를
foo(); // window
const obj = { foo }; // ES6 프로퍼티 축약 표현

// 메서드로서 호출
obj.foo(); // obj

// 생성자 함수로서 호출
const inst = new foo(); // inst
```

</aside>

→ 생성자 함수는 이름 그대로 객체(인스턴스)를 생성하는 함수다.

- 일반 함수와 동일한 방법으로 생성자 함수를 정의하고 new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다.
- 만약 new 연산자와 함께 생성자 함수를 호출하지 않으면 생성자 함수가 아니라 일반 함수로 동작한다.

```jsx
// new 연산자와 함께 호출하지 않으면 생성자 함수로 동작하지 않는다.
// 즉, 일반 함수로서 호출된다.
const circle3 = Circle(15);

// 일반 함수로서 호출된 Circle 은 반환문이 없으므로 암묵적으로 undefined
console.log(circle3); // undefined

// 일반 함수로서 호출된 Circle 내의 this는 전역 객체를 가리킨다.
console.log(radius); // 15
```

</aside>

### **📌 생성자 함수의 인스턴스 생성 과정**

<aside>
💐

→ 생성자 함수의 역할은?

- 프로퍼티 구조가 동일한 인스턴스를 생성하기 위한 템플릿으로서 동작하여 인스턴스를 생성
- 생성된 인스턴스를 초기화

```jsx
// 생성자 함수
function Circle(radius) {
	// 인스턴스 초기화
	this.radius = radius;
	this.getDiameter = function () {
		return 2 * this.radius;
	};
}

// 인스턴스 생성
const circle1 = new Circle(5); // 반지름이 5인 Circle 객체 생성
```

→ this에 프로퍼티 추가

- 전달된 인수를 프로퍼티의 초기값으로 할당 후 인스턴스 초기화

→ 인스턴스를 생성하고 반환하는 코드는 보이지 X

- 자바스크립트 엔진은 암묵적인 처리를 통해 인스턴스를 생성하고 반환.
- new 연산자와 함께 생성자 함수를 호출하면 ? 다음 과정을 거쳐 초기화 후 인스턴스 반환.
1. 인스턴스 생성과 this 바인딩
    - 암묵적으로 빈 객체 생성된다. (생성자 함수가 생성한 인스턴스)
    - 생성된 빈 객체, 인스턴스는 this에 바인딩된다.
    - 생성자 함수 내부의 this가  생성자 함수가 생성할 인스턴스를 가리킨다.
    - 이 처리는 실행되는 런타임 이전에 실행된다.
    
    ```jsx
    function Circle(radius) {
    	// 1. 암묵적으로 인스턴스가 생성 후 this에 바인딩
    	console.log(this); // Circle {}
    
    	this.radius = radius;
    	this.getDiameter = function () {
    		return 2 * this.radius;
    	};
    }
    ```
    
2. 인스턴스 초기화
    - this에 바인딩 되어 있는 인스턴스에 프로퍼티나 메서드를 추가
    - 생성자 함수가 인수로 전달 받은 초기값을 인스턴스 프로퍼티에 할당하여 초기화 및 고정값을 할당
    
    ```jsx
    function Circle(radius) {
    	// 1. 암묵적 인스턴스 생성 후 this 바인딩
    	
    	// 2. this에 바인딩 되어 있는 인스턴스 초기화
    	this.radius = radius;
    	this.getDiameter = function () {
    		return 2 * this.radius;
    	};
    }
    ```
    
3. 인스턴스 반환
    - 생성자 함수 내부의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this 암묵저으로 반환한다.
    
    ```jsx
    // 생성자 함수
    function Circle(radius) {
    	// 1. 암묵적 인스턴스 생성 후 this 바인딩
    	
    	// 2. this에 바인딩 되어 있는 인스턴스 초기화
    	this.radius = radius;
    	this.getDiameter = function () {
    		return 2 * this.radius;
    	};
    	// 3. 완성된 인스턴스가 바인딩된 this를 암묵적으로 반환
    }
    
    // 인스턴스 생성. Circle 생성자 함수는 암묵적으로 this 반환
    const circle = new Circle(1);
    console.log(circle); // Circle { radius: 1, getDiameter: f } 
    ```
    
    - 만약 this가 아닌 다른 객체를 명시적으로 반환하면 this가 반환되지 못하고 return 문에 명시한 객체가 반환된다.
    
    ```jsx
    // 생성자 함수
    function Circle(radius) {
    	// 1. 암묵적 인스턴스 생성 후 this 바인딩
    	
    	// 2. this에 바인딩 되어 있는 인스턴스 초기화
    	this.radius = radius;
    	this.getDiameter = function () {
    		return 2 * this.radius;
    	};
    	// 3. 완성된 인스턴스가 바인딩된 this를 암묵적으로 반환
    	// 명시적으로 객체 반환 this 반환 무시
    	return {};
    }
    
    // 인스턴스 생성. Circle 생성자 함수는 명시적으로 반환한 객체 반환
    const circle = new Circle(1);
    console.log(circle); // {}
    ```
    
    - 하지만 명시적으로 원시 값을 반환하면 원시 값 반환은 무시되고 암묵적으로 this가 반환된다.
    
    ```jsx
    // 생성자 함수
    function Circle(radius) {
    	// 1. 암묵적 인스턴스 생성 후 this 바인딩
    	
    	// 2. this에 바인딩 되어 있는 인스턴스 초기화
    	this.radius = radius;
    	this.getDiameter = function () {
    		return 2 * this.radius;
    	};
    	// 3. 완성된 인스턴스가 바인딩된 this를 암묵적으로 반환
    	// 명시적으로 원시 값 반환 시 무시 암묵적으로 this 반환 
    	return 100;
    }
    
    // 인스턴스 생성. Circle 생성자 함수는 명시적으로 반환한 객체 반환
    const circle = new Circle(1);
    console.log(circle); // Circle { radius: 1, getDiameter: f } 
    ```
    
    → 이처럼 생성자 함수 내부에서 명시적으로 this가 아닌 다른 값을 반환하는 것은 생성자 함수의 기본동작을 훼손한다.
    
    따라서 생성자 함수 내부에서 return 문을 반드시 생략해야 한다.
    
</aside>

### **📌 내부 메서드[[Call]]과 [[Construct]]**

<aside>
➡️

→ 함수 선언문 또는 함수 표현식으로 정의한 함수는 일반적인 함수로서 호출할 수 있고, 생성자 함수로서 호출 할 수 있다.

- 생성자 함수로서 호출이란? → new 연산자와 함께 호출하여 객체를 생성하는 것을 의미

→ 함수는 객체이므로 일반 객체와 동일하게 동작할 수 있다.

- 함수 객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드를 모두 가지고 있기 때문.

```jsx
// 함수는 객체다
function foo() {}

// 함수는 객체이므로 메서드를 소유할 수 있다.
foo.method = function () {
	console.log(this.prop);
};

foo.method(); // 10
```

→ 함수는 객체이지만 일반 객체와는 다르다.

- 일반 객체는 호출할 수 없지만 함수는 호출할 수 있다.
- 함수 객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드와 이외로 추가로 가지고 있다.
- 함수가 일반 함수로서 호출되면 함수 객체의 내부 메서드 [[Call]]이 호출되고 new 연산자와 함께 생성자 함수로서 호출되면 내부 메서드 [[Construct]]가 호출된다.

```jsx
function foo() {}

// 일반적인 함수로서 호출: [[Call]]이 호출된다.
foo();

// 생성자 함수로서 호출: [[Construct]]가 호출된다.
new foo();
```

→ 내부 메서드 [[Call]]을 갖는 함수 객체를 callable이라 하며, 내부 메서드 [[Construct]]를 갖는 함수 객체를 constructor, 갖지않는 함수 객체를 non-constructor라고 부른다.

- callable은 호출할 수 있는 객체, 즉 함수를 말하며, constructor는 생성자 함수로서 호출할 수 있는 함수, non-constructor는 객체를 생성자 함수로서 호출할 수 없는 함수를 의미한다.

→ 모든 함수 객체는 내부 메서드 Call를 갖고 있으므로 호출할 수 있다.

- 그러나 모든 함수 객체가 Construct를 갖는 것은 아니다.
- 함수 객체는 constructor 또는 non-consturctor 이다.
- 즉, 모든 함수 객체는 호출할 수 있지만 모든 함수 객체를 생성자 함수로서 호출할 수 있는 것은 아니다.
</aside>

### **📌 constructor와 non-constructor의 구분**

<aside>
📎

→ 자바스크립트 엔진이 어떻게 constructor와 non-constructor를 구분하는지 살펴보자

- 자바스크립트 엔진은 함수 정의를 평가하여 함수 객체를 생성할 때 함수 정의 방식에 다라 구분한다.
- constructor : 함수 선언문, 함수 표현식, 클래스
- non-constructor : 메서드(ES6 메서드 축약 표현), 화살표 함수

```jsx
// 일반 함수 정의: 함수 선언문, 함수 표현식
function foo() {}
const bar = function () {};
// 프로퍼티 x의 값으로 할당된 것은 일반 함수로 정의된 함수다. 이는 메서드로 인정 X
const baz = { 
	x: function () {}
};

// 일반 함수로 정의된 함수만이 constructor다.
new foo(); // foo {}
new bar(); // bar {}
new baz.x(); // x {}

// 화살표 함수 정의
const arrow = () => {};

new arrow(); // 타입에러

// 메서드 정의: ES6 메서드 축약 표현만 메서드로 인정한다.
const obj = { 
	x() {}
};

new obj.x(); // 타입에러
```

→ 함수를 프로퍼티 값으로 사용하면 일반적으로 메서드로 통칭한다.

- But. ECMAScript 사양에서 메서드란 ES6의 메서드 축약 표현만을 의미한다.
- 함수가 어디에 할당되어 있는지에 따라 메서드인지를 판단하는 것이 아닌 함수 정의 방식에 따라 구분.
- 따라서 위 예제에서 일반 함수, 함수 선언문과 함수 표현식으로 정의된 함수만이 constructor
- ES6의 화살표 함수와 메서드 축약 표현으로 정의된 함수는 non-constructor다.

→ non-constructor인 함수 객체를 생성자 함수로서 호출하면 에러가 발생한다.

```jsx
function foo() {}

// 일반 함수로서 호출
// [[Call]]이 호출된다. 모든 함수 객체는 [[Call]] 이 구현되어 있다.
foo();

// 생성자 함수로서 호출
// [[Construct]]가 호출된다. 이때 [[Construct]]가 없다면 에러가 발생
new foo();
```

→ 주의할 점!

- 생성자 함수로서 호출될 것을 기대하고 정의하지 않은 일반 함수에 new 연산자를 붙여 호출하면 생성자 함수 처럼 동작할 수 도 있다.
</aside>

### **📌 new 연산자**

<aside>
🗣

→ 일반 함수와 생성자 함수에 특별한 형식적 차이는 없다.

- new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다.
- 함수 객체의 내부 메서드 Call 이 아닌 Construct가 호출된다.
- 마찬가지로 non-contructor가 아닌 constructor여야 호출된다.

```jsx
// 생성자 함수로서 정의하지 않은 일반 함수
function add(x, y) {
	return x + y;
}

// 생성자 함수로서 정의하지 않은 일반 함수를 new 연산자와 함께 호출
let inst = new add();

// 함수가 객체를 반환하지 않았으므로 반환문이 무시된다. 따라서 빈 객체 반환
console.log(inst); // {}

// 객체를 반환하는 일반 함수
function createUser(name, role) {
	return { name, role };
}

// 일반 함수를 new 연산자와 함께 호출
inst = new createUser('Lee', 'admin');
// 함수가 생성한 객체를 반환한다.
console.log(inst); // { name: 'Lee', role: 'admin' }
```

→ 반대로 new 연산자 없이 생성자 함수를 호출하면 일반 함수로 호출된다.

```jsx
// 생성자 함수
function Circle(radius) {
	this.radius = radius;
	this.getDiameter = function () {
		return 2 * this.radius;
	};
}

// new 연산자 없이 생성자 함수 호출하면 일반 함수로서 호출된다.
const circle = Circle(5);
console.log(circle); // undefined

// 일반 함수 내부의 this는 전역 객체 window를 가리킨다
console.log(radius); // 5
console.log(getDiameter()); // 10

circle.getDiameter(); // 참조에러 why? window에 있으니까
```

→ Circle 함수를 new 연산자와 함께 생성자 함수로서 호출하면 함수 내부의 this는 Circle 생성자 함수가 생성할 인스턴스를 가리킨다.

- 하지만 Circle 함수를 일반적인 함수로서 호출하면 함수 내부의 this는 전역 객체 window를 가리킨다.
- 위 예제에서 Circle 내부의 this는 전역 객체 window를 가리킨다.
- 따라서 radius 와 getDiameter 는 전역 객체의 프로퍼티와 메서드가 된다.
</aside>

### **📌 new.target**

<aside>
👨‍👩‍👦

→ 생성자 함수가 new 연산자 없이 호출되는 것을 방지하기 위해 파스칼 케이스 컨벤션을 사용한다 싶더라도 실수는 언제나 발생한다. 이러한 위험성을 회피하기 위해 ES6에서 만들어진 문법

new.target 이다.

- new.target은 this와 유사하게 모든 함수 내부에서 암묵적인 지역 변수와 같이 사용
- 메타 프로퍼티라고 불린다. But. IE는 new.target을 지원하지 않는다.
- 함수 내부에서 new.target을 사용하면 new 연산자와 함께 생성자 함수로서 호출되었는지 확인할 수 있다.
- new 연산자와 함께 생성자 함수로서 호출되면 함수 내부의 new.target은 함수 자신을 가리킨다.
- new 연산자 없이 일반 함수로서 호출된 함수 내부의 new.target은 undefined이다.

```jsx
// 생성자 함수
function Circle(radius) {
	// 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined이다.
	if(!new.target){
		// new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환.
		return new Circle(radius);
	}
	this.radius = radius;
	this.getDiameter = function () {
		return 2 * this.radius;
	};
}

// new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출
const circle = Circle(5);
console.log(circle.getDiameter());
```

→ new 연산자와 함께 생성자 함수에 의해 생성된 객체는 프로토 타입에 의해 생성자 함수와 연결된다.

- 이를 이용해 new 연산자와 함께 호출되었는지 확일 할 수 있다.
- 참고로 대부분의 빌트인 생성자 함수는 new 연산자와 함께 호출되었는지를 확인한 후 적절한 값을 반환한다.

```jsx
let obj = new Object();
console.log(obj); // {}

obj = Object();
console.log(obj); // {}

let f = new Function('x', 'return x ** x');
console.log(f); // f anonymous(x) { return x ** x }

f = Function('x', 'return x ** x');
console.log(f); // f anonymous(x) { return x ** x }
```

```jsx
// new 연산자 없이 호출 시 데이터 타입을 변환
const str = String(123);
console.log(str, typeof str); // 123 string

```

</aside>