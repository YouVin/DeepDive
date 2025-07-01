### ⭐️24 클로저

<aside>
🎅

→ 클로저는 자바스크립트 고유의 개념이 아니다.

- 함수를 일급 객체로 취급하는 함수형 프로그래밍 언어에서 사용되는 중요한 특성이다.
- MDN에서 클로저는 함수와 그 함수가 선언된 렉시컬 환경과의 조합이다.

→ 핵심 키워드는 함수가 선언된 렉시컬 환경이다.

```jsx
const x = 1;
function outerFunc() {
	const x = 10;
	innerFunc();
}

function innerFunc() {
	console.log(x); // 1
}

outerFunc();
```

→ innerFunc 함수를 outerFunc 내부에서 호출 하였다 하더라도 함수 변수까지는 접근이 불가능하다.

- 이는 자바스크립트가 렉시컬 스코프를 따르는 프로그래밍 언어이기 때문이다.
</aside>

### ⭐️24.1 렉시컬 스코프

<aside>
🎅

→ 자바스크립트 엔진은 함수를 어디서 호출했는지가 아니라 함수를 어디에 정의했는지에 따라 상위 스코프를 결정한다. → 이를 렉시컬 스코프라 한다.

- 스코프의 실체는 실행 컨텍스트의 렉시컬 환경이다.
- 렉시컬 환경은 자신의 외부 렉시컬 환경에 대한 참조를 통해 상위 렉시컬 환경과 연결된다.
- 함수의 상위 스코프를 결정하는 것은 외부 렉시컬 환경에 대한 참조에 저장할 참조값이 바로 상위 렉시컬 환경에 대한 참조이며, 상위스코프이다.

→ 렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장할 참조값,
즉 상위 스코프에 대한 참조는 함수 정의가 평가되는 시점에 함수가 정의된 환경에 의해 결정된다.

이것이 바로 렉시컬 스코프다.

</aside>

### ⭐️24.2 함수 객체의 내부 슬롯 [[Environment]]

<aside>
🎅

→ 함수가 정의된 환경과 노출되는 환경은 다를 수 있다.

- 따라서 렉시컬 스코프가 가능하려면 함수는 자신이 정의된 환경, 상위 스코프를 기억해야 한다.
- 이를 위해 함수는 자신의 내부슬롯[[Environment]]에 자신이 정의 된 환경, 상위 스코프의 참조를 저장한다.

→ [[Environment]] 담기는 순서

1. 함수 정의 평가
2. 함수 객체 생성
3. 정의된 환경에 의해 결정된 상위 스코프 참조를 내부 슬롯 [[Environment]]에 저장
4. [[Environment]] 저장된 상위 스코프 참조는 실행 컨텍스트의 렉시컬 환경을 가리킨다.

→ 왜 실행 컨텍스트의 렉시컬 환경을 가리켜?

- 함수 객체를 생성하는 시점은 함수가 정의된 환경, 상위 함수가 평가  또는 실행되고 있는 시점이며, 이때 실행 컨텍스트는 해당 상위 함수의 실행 컨텍스트 이기 때문이다.
- 함수 객체의 내부 슬롯 [[Environment]]에 저장된 현재 실행 중인 실행 컨텍스트의 렉시컬 환경의 참조가 바로 상위 스코프다.
- 또한 자신이 호출되었을 때 생성될 함수 렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장될 참조값이다.
- 함수 객체는 내부슬롯 [[Environment]]에 저장한 렉시컬 환경의 참조, 즉 상위 스코프를 자신이 존재하는 한 기억한다.

→ 함수가 호출되면 함수 내부로 코드의 제어권이 이동한다. 그리고 함수 코드를 평가하기 시작한다. 함수 코드 평가는 아래 순서로 진행된다.

1. 함수 실행 컨텍스트 생성
2. 함수 렉시컬 환경 생성
    
    2.1 함수 환경 레코드 생성
    
    2.2 this 바인딩
    
    2.3 외부 렉시컬 환경에 대한 참조 결정
    

→ 외부 렉시컬 환경에 대한 참조에는 함수 객체의 내부 슬롯에 [[Environment]]에 저장된 렉시컬 환경의 참조가 할당 된다.

</aside>

### ⭐️24.3 클로저와 렉시컬 환경

<aside>
🎅

```jsx
const x = 1;

// 1 
function outer() {
	const x = 10;
	const inner = function () { console.log(x); }; // 2
	return inner;
}

// outer 함수를 호출하면 중첩 함수 inner를 반환한다.
// 그리고 outer 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 팝되어 제거된다.
const innerFunc = outer(); // 3
innerFunc(); // 4 -> 10
```

→ 3번에서 outer() 함수는 inner를 return 하고 생명 주기를 마감한다.

- outer 함수의 실행 컨텍스트는 스택에서 제거된다.
- 스택에 제거된 함수에서 x와 변수 값 10 또한 실행 컨텍스트에서 제거되어 생명주기를 마감한다.
- outer 함수의 지역 변수 x 는 더는 유효하지 않아 접근 방법은 없어보인다.

→ 그러나 4번을 보면? 지역 변수 x 가 부활했다?

- 이처럼 외부 함수보다 중첩 함수가 더 오래 유지되는 경우 중첩 함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조할 수 있다.
- 이러한 중첩 함수를 클로저라고 부른다.

→ MDN ( 클로저는 함수와 그 함수가 선언된 렉시컬 환경과의 조합이다. )

클로저가 발생하는 방식은 무엇일까 ?

1. inner 함수는 자신이 평가될 때 자신이 정의된 위치에 의해 결정된 상위 스코프를 [[Environment]] 내부 슬롯에 저장한다.
2. outer 함수가 평가되어 함수 객체를 생성할 때 (1) 현재 실행 중인 실행 컨텍스트의 렉시컬 환경, 즉 전역 렉시컬 환경을 outer 함수 객체의 [[Environment]] 내부 슬롯에 상위 스코프로서 저장한다.
3. 그리고 중첩 함수 inner가 평가된다. (2) 이때 중첩 함수 inner는 자신의 [[Environment]] 내부 슬롯에 현재 실행 중인 실행 컨텍스트의 렉시컬 환경 outer 함수의 렉시컬 환경을 상위 스코프로서 저장한다.
4. outer 함수가 종료되고, inner 함수를 반환, outer의 생명 주기는 끝이난다.(3) 스택에서 제거되지만 outer 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 제거되지만 outer 함수의 렉시컬 환경까지 소멸하는 것은 아니다.
5. 바로 (2)에서 inner 함수의 [[Environment]] 내부 슬롯에서 참조되고 있고 inner 함수는 전역 변수 innerFunc에 의해 참조되고 있으므로 가비지 컬렉션의 대상이 되지 않는다.

→ 이렇게 중첩 함수 inner는 외부 함수 outer 보다 더 오래 생존했다.

- 외부 함수보다 더 오래 생존한 중첩 함수는 외부 함수의 생존 여부와 상관없이 자신이 정의된 위치에 의해 결정된 상위 스코프를 기억한다.
- 중첩 함수 inner의 내부에서는 상위 스코프를 참조할 수 있으므로 상위 스코프의 식별자를 참조할 수 있고 식별자의 값을 변경할 수도 있다.

→ 자바스크립트의 모든 함수는 상위 스코프를 기억하므로, 이론적으로 모든 함수는 클로저다.
But. 일반적으로 모든 함수를 클로저라고 하지는 않는다.
다음과 같은 예제가 있다.

1. 상위 스코프의 어떤 식별자도 참조하지 않는 경우 대부분의 모던 브라우저는 최적화를 통해 상위 스코프를 기억하지 않는다.
참조하지도 않는 식별자를 기억하는 것은 메모리 낭비이기 때문이다.
2. 상위 스코프의 식별자를 참조하지만, 외부 함수보다 중첩 함수의 생명 주기가 짧을 경우, 해당 함수는 클로저 였지만, 외부 함수보다 일찍 소멸되기 때문에 생명 주기가 종료된 외부 함수의 식별자를 참조할 수 있다는 클로저의 본질에 부합하지 않는다.

→ 클로저는 중첩 함수가 상위 스코프의 식별자를 참조하고 있고 중첩 함수가 외부 함수보다 더 오래 유지되는 경우에 한정하는 것이 일반적이다.

</aside>

### ⭐️24.4 클로저의 활용

<aside>
🎅

→ 클로저의 활용을 살펴보자!

- 클로저는 상태를 안정하게 변경하고 유지하기 위해 사용한다.
→ 상태가 의도치 않게 변경되지 않도록 상태를 안전하게 은닉하고 특정 함수에게만 상태 변경을 허용한다.

```jsx
// 카운트 상태 변수
let num = 0;

// 카운트 상태 변경 함수
const increase = function () {
	// 카운트 상태를 1만큼 증가시킨다.
	return ++num;
};

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```

→ 위 코드의 문제점 (의존성)

1. 카운트 상태 (num 변수의 값)는 increase 함수가 호출되기 전까지 변경되지 않고 유지되어야 한다.
2. 이를 위해 카운트 상태는 increase 함수만이 변경할 수 있어야 한다.

→ 근데? num은 전역 변수이기에 누구든 접근하고 변경할 수 있다.

- 이는 의도치 않게 상태가 변경될  수 있다는 것을 의미한다.
- 만약 누군가에 의해 의도치 않게 카운트 상태, 전역 변수 num의 값이 변경되면 이는 오류로 이어진다.
- 따라서 카운트 상태를 안전하게 하기 위해서는 increase 함수만이 num 변수를 참조하여 변경할 수 있어야 한다.

→ 그러면 안에다가 두면 되는거 아냐?

```jsx
// 카운터 상태 변경 함수
const increase = function () {
	// 카운트 상태 변수
	let num = 0;
	
	// 카운트 상태를 1만큼 증가시킨다.
	return ++num;
};

// 이전 상태를 유지하지 못한다.
console.log(increase()); // 1
console.log(increase()); // 1
console.log(increase()); // 1
```

→ 왜이렇게 되나? 

- 의도치 않은 상태 변경은 방지되었지만, increase 함수가 호출될 때마다 지역 변수 num은 다시 선언되고 0으로 초기화 되기 때문에 출력 결과가 언제나 1이다.
- 따라서 상태가 변경되기 이전 상태를 유지하지 못한다. 이때 클로저를 사용해보자

→ 클로저 활용

```jsx
// 카운터 상태 변경 함수
const increase = (function () {
	// 카운터 상태 변수
	let num = 0;
	// 클로저
	return function () {
		// 카운트 상태를 1만큼 증가시킨다.
		return ++num;
	};
}());

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```

→ 클로저의 장점과 순서

- 즉시 실행 함수로 만들어진 increase는 호출 된 이후 바로 소멸하지만, 즉시 실행 함수가 반환한 클로저는 increase 변수에 할당되어 호출된다.
- 이때 반환한 클로저는 상위 스코프 렉시컬 환경을 기억하고 있다, 따라서 카운트 상태를 유지하기 위한 num을 언제 어디서 호출하든지 참조하고 변경할 수 있다.
- 이때 num 변수는 즉시 실행 함수 내에서 한번만 사용되어 재차 초기화 될 일은 없을 것이다. 또한 외부에서 직접 접근도 불가능한 은닉된 private 변수가 된다.

→ 이처럼 클로저는 상태가 의도치 않게 변경되지 않도록 안전하게 은닉하고 특정 함수에게만 상태 변경을 허용하여 상태를 안전하게 변경하고 유지하기 위해 사용된다.

- 추가로 카운트 상태를 감소하는 코드도 추가해보자

```jsx
const counter = (function () {
	// 카운트 상태 변수
	let num = 0;
	
	// 클로저인 메서드를 갖는 객체를 반환한다.
	// 객체 리터럴은 스코프를 만들지 않는다.
	// 따라서 아래 메서드들의 상위 스코프는 즉시 실행 함수의 렉시컬 환경이다.
	return {
		// num: 0 // 프로퍼티는 public으로 은닉되지 않는다.
		increase() {
			return ++num;
		},
		decrease() {
			return num > 0 ? --num : 0;
		}
	};
}());

console.log(counter.increase()); // 1
console.log(counter.increase()); // 2
console.log(counter.decrease()); // 1
console.log(counter.decrease()); // 0
```

→ 여기서 사용된 객체 리터럴은 별도의 스코프를 생성하지 않는다.

- 각 increase, decrease 가 평가되는 시점에 상위 스코프는 즉시 실행 함수 실행 컨텍스트의 렉시컬 환경이다.
- 따라서 각 함수들은 언제 어디서든 즉시 실행 함수의 스코프의 식별자를 참조할 수 있다.

→ 위 예제를 생성자 함수로 바꿔보자

```jsx
const Counter = (function () {
	// 1 카운트 상태 변수
	let num = 0;
	
	function Counter() {
		// this.num = 0; // 2 프로퍼티는 public 은닉되지 않는다.
	}
	
	Counter.prototype.increase = function () {
		return ++num;
	};
	
	Counter.prototype.decrease = function () {
		return num > 0 ? --num : 0;
	};
	
	return Counter;
}());

const counter = new Counter();

console.log(counter.increase()); // 1
console.log(counter.increase()); // 2
console.log(counter.decrease()); // 1
console.log(counter.decrease()); // 0
```

1. num은 생성자 함수가 생성할 인스턴스의 프로퍼티가 아니라 즉시 실행 함수 내에서 선언된 변수이다.
2. Counter 는 프로토타입을 통해 각 increase, decrease 메서드를 상속받는 인스턴스를 생성한다.
3. 각 메서드는 즉시 실행 함수 실행 컨텍스트의 렉시컬 환경을 기억하는 클로저다.
4. 따라서 자유 변수 num 값은 increase, decrease 메서드만이 변경할 수 있다.

→ 함수형 프로그래밍에서 활용하는 클로저

```jsx
function makeCounter(helperFn) {
  let counter = 0; // 🔐 이 변수는 makeCounter 안에서만 존재하는 지역 변수야

  return function () {
    counter = helperFn(counter); // 🔁 이 함수가 counter 값을 변경
    return counter;
  };
}

// 보조 함수들
const increase = (n) => n + 1;
const decrease = (n) => n - 1;

// 각각의 카운터 생성
const up = makeCounter(increase);
const down = makeCounter(decrease);

console.log(up());   // 1
console.log(up());   // 2
console.log(down()); // -1
console.log(down()); // -2
```

🔹 1. `makeCounter` 안에 `counter = 0` 있음

- 이건 원래라면 `makeCounter` 실행 끝나면 사라져야 해

🔹 2. 그런데, 안에서 `function () { ... }` 이 함수가 `counter`를 쓰고 있음

- 그 함수가 밖으로 리턴되니까
- 자바스크립트는 “어 이 변수 나중에도 필요하네?” 하고 **안 지움**
- 이게 바로 **클로저**야

🔹 3. 그 함수는 `counter`에 접근 가능하고, 계속 유지함

- `up()`과 `down()`은 **서로 다른 렉시컬 환경에서 만들어졌기 때문에**,
    
    각자의 `counter` 값을 따로 기억해!
    

→ 결론

> makeCounter()는 실행 시 counter라는 지역 변수를 가진 렉시컬 환경을 생성하고
> 
> 
> 내부 함수는 그 환경을 **[[Environment]] 슬롯에 저장**
> 
> 이 함수가 클로저가 되어 **그 변수에 계속 접근 가능**
> 
> `makeCounter()`를 다시 호출하면 **서로 다른 환경을 가지는 독립적인 클로저들이 생성**됨
> 

→ 다음은 클로저 환경을 공유하는 예제로 바꿔보자

```jsx
// makeCounter: 클로저를 하나만 만들고, 보조 함수로 상태 변경을 위임
function makeCounter() {
  let counter = 0; // 🔐 공유될 상태 (클로저 환경 안에 있음)

  // 이 함수는 여러 보조 함수를 받아서 counter를 조작
  return function (helperFn) {
    counter = helperFn(counter);
    return counter;
  };
}

// 👉 클로저 함수 하나만 만들기 (이게 상태를 기억함)
const counterFn = makeCounter();

// 👈 보조 함수들을 필요할 때 넘겨줌
const up = () => counterFn(n => n + 1);
const down = () => counterFn(n => n - 1);

// 사용
console.log(up());   // 1
console.log(up());   // 2
console.log(down()); // 1 ✅ 공유된 counter 사용
console.log(up());   // 2 ✅ 계속 이어짐

```

- `makeCounter()` → 한 번만 호출
- `counter` → 클로저 환경에서 살아남아 공유됨
- `up`, `down` → 같은 `counterFn`을 호출하므로 같은 상태 사용
</aside>

### ⭐️24.5 캡슐화와 정보 은닉

<aside>
🎅

→ 캡슐화란?

- 객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 조작할 수 있는 동작인 메서드를 하나로 묶는 것을 말한다.
- 캡슐화는 객체의 특정 프로퍼티나 메서드를 감출 목적으로  사용하기도 하는도 하는데 이를 정보 은닉이라 한다.

→ 정보 은닉이란?

- 외부에 공개할 필요가 없는 구현의 일부를 외부에 공개되지 않도록 감추어 적절치 못한 접근으로부터 객체의 상태가 변경되는 것을 방지해 정보를 보호하고, 객체 간의 상호 의존성, 즉 결합도를 낮추는 효과가 있다.

→ 접근 제한자?

- 자바스크립트는 public, private, protected 같은 접근 제한자를 제공하지 않는다.
- 자바스크립트 객체의 모든 프로퍼티와 메서드는 기본적으로 외부에 공개되어 있다. 기본적으로 public이다.

```jsx
function Person(name, age) {
	this.name = name; // public
	let _age = age; // private
	
	// 인스턴스 메서드
	this.sayHi = function () {
		console.log(`Hi! My name is ${this.name}. I am ${_age}/`);
	};
}

const me = new Person('Lee', 20);
me.sayHi(); // Hi! My name is Lee. I am 20.
console.log(me.name); // Lee
console.log(me._age); // undefined

const you = new Person('Kim', 30);
you.sayHi(); // Hi! My name is Kim. I am 20.
console.log(you.name); // Kim
console.log(you._age); // undefined
```

→ name은 외부 공개로 자유롭게 참조 변경 가능

- _age 변수는 지역 변수로 생성자 함수 외부에서는 참조하거나 변경이 불가능 하다.
- 즉 _age 변수는 private하다.
- But. Person 객체가 생성될 때마다 중복 생성된다.

→ 중복 생성 방지하기

```jsx
function Person(name, age) {
	this.name = name; // public
	let _age = age; // private
}

// 프로토타입 메서드
Person.prototyep.sayHi = function () {
	// Person 생성자 함수의 지역 변수 _age를 참조할 수 없다.
	console.log(`Hi! My name is ${this.name}. I am ${_age}`);
};
```

→ 프로토타입으로 만드러서 할 경우 생성자 함수의 지역 변수 _age를 참조할 수 없는 문제가 발생한다. 따라서 즉시 실행 함수를 사용하여 하나의 함수 내에 모아야 한다.

```jsx
const Person = (function () {
	let _age = 0; // private
	
	// 생성자 함수
	function Person(name, age) {
	this.name = name; // public
	let _age = age; 
	}
	
	// 프로토타입 메서드
	Person.prototyep.sayHi = function () {
		console.log(`Hi! My name is ${this.name}. I am ${_age}`);
	};
	
	// 생성자 함수을 반환
	return Person;
}());

const me = new Person('Lee', 20);
me.sayHi(); // Hi! My name is Lee. I am 20.
console.log(me.name); // Lee
console.log(me._age); // undefined

const you = new Person('Kim', 30);
you.sayHi(); // Hi! My name is Kim. I am 20.
console.log(you.name); // Kim
console.log(you._age); // undefined
```

→ 위와 같이 하면 age 참조도 가능하고, 정보 은닉도 가능해 보인다

- But. 버그 하나 발생 _age 변수 값이 변경되는 오류 발생 !!
- 위 예제에서 마지막 코드에 me.sayHi(); 로 하면 _age는 30이 나오게 된다.
- 이는 클로저로 자유 변수 num이 공유되어 발생하는 문제다.
- 이처럼 자바스크립트는 정보 은닉을 완전하게 지원하지 않는다.
</aside>

### ⭐️24.6 자주 발생하는 실수

<aside>
🎅

→ 클로저를 사용할 때 자주하는 실수 모음

```jsx
var funcs = [];

for(var  i = 0; i < 3; i++){
	funcs[i] = function () { return i; }; // 1
}

for (var j = 0; j < funcs.length; j++) {
	console.log(funcs[j]()); // 2
}
```

→ 여기서 funcs[j] 에서 담아온 값이 0, 1, 2를 기대했지만, 결과는 그렇지 않다.

- var 키워드로 선언한 i 변수는 블록 레벨이 아닌 함수 레벨 스코프를 갖기 때문에 전역 변수다.
- 전역 변수 i에 순차적으로 0, 1, 2 값이 할당되며, funcs 배열의 요소로 추가한 함수를 호출하면 전역 변수 i를 참조하여 i 의 값 3이 출력된다.

→ 클로저를 통해 바르게 동작하도록 바꾸자

```jsx
var funcs = [];

for (var i = 0; i < 3; i++) {
	funcs[i] = (function (id) { // 1
		return function () {
			return id;
		};
	}(i));
}

for (var j = 0; j < funcs.length; j++) {
	console.log(funcs[j]());
}
```

→ 순차적으로 확인하기

1. 즉시 실행 함수 1은 전역 변수 i에 현재 할당되어 있는 값 → 인수로 전달 받은 매개변수 id에 할당하고 함수를 종료한다.
2. 즉시 실행 함수가 반환한 함수는 funcs 배열에 순차적으로 저장된다.
3. 즉시 실행 함수가 반환한 중첩 함수는 자신의 상위 스코프를 기억하는 클로저로 매개변수 id는 자유 변수가 되어 그 값이 유지된다.

→ 간단하게 ES6 문법 let 키워드 활용하자.

```jsx
const funcs = [];
for(let i = 0; i < 3; i++) {
	funcs[i] = function () { return i; };
}

for(let i = 0; i < funcs.length; i++) {
	console.log(funcs[i]()); // 0 1 2
}
```

→ let은 왜 이게 가능한가?

1. for문 평가시 let 키워드로 선언한 변수는 렉시컬 환경을 생성하고 초기화 변수 식별자와 값을 등록한다.
2. 새롭게 생성된 렉시컬 환경을 현재 실행 중인 실행 컨텍스트의 렉시컬 환경으로 교체한다.
3. for문이 코드 블록이 반복 실행 하면서 새로운 렉시컬 환경을 생성하고 식별자 id에 증감문 반영 이전을 등록한다.
4. 새롭게 생성된 렉시컬 환경을 현재 실행 중인 실행 컨텍스트와 교체한다.
5. 반복문이 종료되면 for 문이 실행되기 이전의 렉시컬 환경을 실행 중인 실행 컨텍스트의 렉시컬 환경으로 되돌린다.

→ 결론

- let 이나 const 키워드로 사용하는 반복문은 코드 블록을 반복 실행 할 때마다 새로운 렉시컬 환경을 생성하여 반복할 당시의 상태를 마치 스냅숏을 찍는 것처럼 저장한다.
- 단 이는 반복문의 코드 블록 내부에서 함수를 정의할 때 의미가 있다.
- 반복문의 코드 블록 내부에 함수 정의가 없는 반복문이 생성하는 새로운 렉시컬 환경은 반복 직후 아무도 참조하지 않기 때문에 가비지 컬렉션이 된다.
</aside>