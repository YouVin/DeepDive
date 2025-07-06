### ⭐️25.1 클래스는 프로토타입의 문법적 설탕인가?

<aside>
💵

→ 프로토타입 기반 객체지향 언어는 클래스가 필요없는 객체지향 프로그래밍 언어다.

But. 클래스 기반 프로그래머들은 프로토타입 기반 방식에 혼란을 받으며 자바스크립트를 어렵게 느꼈다.

이를 해결하기 위해 ES6에서 클래스를 도입하였다.

→ ES6 클래스는?

- 클래스는 함수이며 기존 프로토타입 기반 패턴을 클래스 기반 패턴처럼 사용할 수 있도록 하는 문법적 설탕이다.
- 클래스와 생성자 함수는 모두 프로토타입 인스턴스를 생성하지만 동일하게 동작하지는 않는다.

→ 클래스와 생성자 함수의 차이점

1. 클래스는 NEW 연산자 없이 호출하면 에러가 발생한다. 생성자 함수는 new 없이 호출하면 일반 함수로 호출된다.
2. 클래스는 상속을 지원하는 extends와 super 키워드를 제공한다. 생성자 함수는 없다.
3. 클래스는 호이스팅일 발생하지 않는 것처럼 동작한다. 생성자 함수는 함수 선언문은 함수 호이스팅, 함수 표현식은 변수 호이스팅이 발생한다.
4. 클래스 내의 모든 코드는 암묵적으로 strict mode이다(해제 불가). 생성자 함수는 아니다.
5. 클래스의 constructor, 프로토타입 메서드, 정적 메서드는 모두 프로퍼티 어트리뷰트 [[Enumerable]] 값이 false이다, 열거가 불가능이다.

→ 따라서 클래스를 새로운 객체 생성 메커니즘으로 보는 것이 더 합당하다. 

</aside>

### ⭐️25.2 클래스 정의

<aside>
💵

→ 클래스는 class 키워드를 사용하여 정의한다. 

- 일반적으로 파스칼 케이스를 사용한다.
- `class Person {}`

→ 일반적이지는 않지만 함수와 마찬가지로 표현식으로 클래스를 정의할 수 도 있다.

```jsx
// 익명 클래스 표현식
const Person = class {};
// 기명 클래스 표현식
const Person = class MyClass {};
```

→ 클래스는 일급 객체이다.

1. 무명의 리터럴로 생성할 수 있다. 즉 , 런타임에 생성이 가능하다.
2. 변수나 자료구조에 저장할 수 있다.
3. 함수의 매개변수에게 전달할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.

→ 클래스 몸체에서 정의할 수 있는 메서드는 constructor(생성자), 프로토타입 메서드, 정적 메서드의 세 가지가 있다.

```jsx
// 클래스 선언문
class Person {
	// 생성자
	constructor(name) {
		// 인스턴스 생성 및 초기화
		this.name = name; // name 프로퍼티는 public하다.
	}
	// 프로토타입 메서드
	sayHi() {
		console.log(`Hi! My name is ${this.name}`);
	}
	// 정적 메서드
	static sayHello(){
		console.log('Hello');
	}
}

// 인스턴스 생성
const me = new Person('Lee');
// 인스턴스의 프로퍼티 참조
console.log(me.name); // Lee
// 프로토타입 메서드 호출
me.sayHi(); // Hi! My name is Lee
// 정적 메서드 호출
Person.sayHello(); // Hello!
```

</aside>

### ⭐️25.3 클래스 호이스팅

<aside>
💵

→ 클래스 선언문으로 정의한 클래스

- 소스코드 평가 과정, 런타임 이전에 먼저 평가되어 함수 객체를 생성한다.
- 클래스로 평가되어 생성된 함수 객체는 생성자 함수로서 호출할 수 있는 constructor이다.
- 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다. 프로토타입과 생성자 함수는 단독으로 존재하지 못하면 언제나 쌍으로 존재한다.

→ 단 클래스는 클래스 정의 이전에 참조할 수 없다.

```jsx
console.log(Person);
// 참조 에러

// 클래스 선언문
class Person {}
```

→ 클래스 선언문은 마치 호이스팅이 발생하지 않는 것처럼 보인다.

```jsx
const Person = '';

{
	// 호이스팅이 발생하지 않는다면 ''이 출력되어야 한다.
	console.log(Person);
	// 참조에러
}

// 클래스 선언문
class Person {}
```

→ 클래스 선언문도 호이스팅이 발생한다. 

- 단 클래스는 let const 키워드로 선언한 변수처럼 호이스팅된다.
- 따라서 선언문 이전에 일시적 사각지대(TDZ)에 빠지기 때문에 호이스팅이 발생하지 않는 것처럼 동작한다.
- var let const function class 키워드로 선언한 모든 식별자는 호이스팅이 된다.
</aside>

### ⭐️25.4 인스턴스 생성

<aside>
💵

→ 클래스는 생성자 함수 new 연산자와 함께 호출하여 인스턴스 생성

- 클래스는 인스턴스를 생성하는 것이 유일한 존재 이유이므로 반드시 new 연산자와 함께 호출해야 한다.

```jsx
class Person {}
// 클래스를 new 연산자 없이 호출하면 타입 에러가 발생한다.
const me = Person();
// 타입에러
```

- 클래스 표현식으로 정의된 클래스의 경우 클래스를 가리키는 식별자를 사용해 인스턴스를 생성하지 않고 기명 클래스 표현식의 클래스 이름을 사용해 인스턴스를 생성하면 에러가 발생한다.

```jsx
const Person = class MyClass {};
// 함수 표현식과 마찬가지로 클래스를 가리키는 식별자로 인스턴스를 생성해야 한다.
const me = new Person();
// 클래스 이름 MyClass는 함수와 동일하게 클래스 몸체 내부에서만 유효한 식별자다.
console.log(MyClass); // 참조에러

const you = new MyClass(); // 참조 에러
```

→클래스 표현식에서 사용한 클래스 이름은 외부 코드에서 접근 불가능하기 때문이다.

</aside>

### ⭐️25.5 메서드

<aside>
💵

→ 클래스 몸체에는 0개 이상의 메서드만 선언할 수 있다. + 정의할 수 있는 메서드 3

1. constructor(생성자)
2. 프로토타입 메서드
3. 정적 메서드
</aside>

### **📌 25.5.1 constructor**

<aside>
💵

→ constructor는 인스턴스를 생성하고 초기화하기 위한 특수한 메서드다. 이름 변경이 불가능하다.

```jsx
class Person {
	// 생성자
	constructor(name) {
		// 인스턴스 생성 및 초기화
		this.name = name;
	}
}
```

→ 클래스는 함수다

`console.log(typeof Person); // function`

- 클래스는 평가되어 함수 객체가 된다.
- 함수 객체 고유의 프로퍼티를 모두 가지고 있다.
- 프로토타입과 연결되어 있으며 자신의 스코프 체인을 구성한다.

→ 클래스가 생성한 인스턴스를 들여다보자

```jsx
// 인스턴스 생성
const me = new Person('Lee');
console.log(me); // constructor는 Person을 가리키고, 프로토타입 name에는 'Lee'가 들어간다.

```

→ constructor는 메서드로 해석되는 것이 아니라 클래스가 평가되어 생성한 함수 객체 코드의 일부가 된다.

- 클래스 정의가 평가되면 constructor의 기술된 동작을 하는 함수 객체가 생성된다.
- 클래스 constructor 와 프로토타입 constructor는 이름만 같을 뿐 연관은 없다.

→ constructor는 생성자 함수와 유사하지만 몇 가지 차이가 있다.

- constructor는 클래스 내에 최대 한 개만 존재할 수 있다. 2개 이상일 경우 문법 에러가 발생
- constructor는 생략이 가능하다. → 생략 시 암묵적으로 빈 constructor가 정의된다.

→ constructor 사용법

1. 프로퍼티로 추가하여 초기화된 인스턴스 생성하기

```jsx
class Person {
	constructor() {
		// 고정값으로 인스턴스 초기화
		this.name = 'Lee';
		this.address = 'Seoul';
	}
}

// 인스턴스 프로퍼티가 추가된다.
const me = new Person();
console.log(me); // Person{ name:'Lee', address:'Seoul' }
```

1. 인스턴스 생성 때 클래스 외부에서 프로퍼티의 초기값 전달하기.

```jsx
class Person {
	constructor(name, address) {
		// 인수로 인스턴스 초기화
		this.name = name;
		this.address = address;
	}
}

// 인수로 초기값을 전달한다.
const me = new Person('Lee', 'Seoul');
console.log(me); // Person{ name:'Lee', address:'Seoul' }
```

- 인스턴스를 초기화하려면 construcotr를 생략해서는 안 된다.

→ constructor는 별도의 반환문이 필요 없다.

- new 연산자와 함께 클래스가 호출되면 생성자 함수와 동일하게 암묵적으로 this, 즉 인스턴스를 반환하기 때문이다.
- 만약 this가 아닌 다른 객체를 명시적으로 반환하면 this, 인스턴스가 반환되지 못하고 return 문에 명시한 객체가 반환된다.
- 하지만 명시적으로 원시값을 반환하면 원시값 반환은 무시되고, 암묵적으로 this가 반환된다.

→ constructor 내부에서 명시적으로 this가 아닌 다른 값을 반환하는 것은 클래스의 기본 동작을 훼손한다!.

따라서 constructor 내부에서 return 문을 반드시 생략해야 한다.

</aside>

### **📌 25.5.2 프로토타입 메서드**

<aside>
💵

→ 생성자 함수를 사용하여 인스턴스 생성 시에 → 프로토타입 메서드를 생성하기 위해서는 명시적으로 추가하기

```jsx
function Person(name) {
	this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHi = function() {
	console.log(`Hi! My name is ${this.name}`);
};

const me = new Person('Lee');
me.sayHi(); // Hi! My name is Lee
```

- 클래스 몸체에서 정의한 메서드는 생성자 함수에 의한 객체 생성과는 다르게 클래스의 prototype 메서드를 추가하지 않아도 기본적으로 프로토타입 메서드가 된다.
- 클래스가 생성한 인스턴스는 생성자 함수와 마찬가지로 프로토타입 체인의 일원이 된다.

→ 클래스 몸체에서 정의한 메서드

- 인스턴스의 프로토타입에 존재하는 프로토타입 메서드가 된다.
- 인스턴스는 프로토타입 메서드를 상속받아 사용할 수 있다.
- 프로토타입 체인은 기존의 모든 객체 생성 방식 뿐만 아니라 클래스에 의해 생성된 인스턴스에도 동일하다.
- 클래스는 인스턴스를 생성하는 생성자 함수라고 볼 수 있다.
</aside>

### **📌 25.5.5 정적 메서드**

<aside>
💵

→ 정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있는 메서드이다.

- 생성자 함수의 경우 정적 메서드를 생성하기 위해서는 명시적으로 생성자 함수에 메서드를 추가해야 한다.
- 클래스에서는 메서드에 static 키워드를 붙이면 정적 메서드가 된다.

```jsx
class Person {
	// 생성자
	constructor(name) {
		this.name;
	}
	
	// 정적 메서드
	static sayHi() {
		console.log('Hi');
	};
}
```

→ 정적 메서드는 클래스에 바인딩된 메서드가 된다.

- 클래스는 함수 객체로 평가되므로 자신의 프로퍼티/메서드를 소유할 수 있다.
- 정적 메서드는 클래스 정의 이후 인스턴스를 생성하지 않아도 호출할 수 있다.
- `Person.sayHi();` 처럼 클래스로 호출한다.

→ 정적 메서드는 인스턴스로 호출할 수 없다.

- 정적 메서드가 바인딩된 클래스는 인스턴스의 프로토타입 체인상에 존재하지 않는다.
- 인스턴스로 클래스의 메서드를 상속 받을 수 없다.

```jsx
// 인스턴스 생성
const me = new Person('Lee');
me.sayHi(); // 타입 에러
```

</aside>

### **📌 25.5.4 정적 메서드와 프로토타입 메서드의 차이**

<aside>
💵

→ 정적 메서드와 프로토타입 메서드의 차이점

1. 정적메서드와 프로토타입 메서드는 자신이 속해 있는 프로토타입 체인이 다르다.
2. 정적 메서드는 클래스로 호출하고 프로토타입 메서드는 인스턴스로 호출한다.
3. 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있다. 

```jsx
class Square {
	constructor(width, height) {
		this.width = width;
		this.height = height;
	}
	
	// 프로토타입 메서드
	area() {
		return this.width * this.height;
	}
}

const square = new Square(10, 10); 
console.log(square.area()); // 100
```

→ 정적 메서드는 클래스로 호출해야 하므로 정적 메서드 내부의 this는 인스턴스가 아닌 클래스를 가리킨다. 즉, 프로토타입 메서드와 정적 메서드 내부의 this 바인딩이 다르다.

- 따라서 메서드 내부에서 인스턴스 프로퍼티를 참조할 필요가 있다면, this를 사용해야하며, 이 경우 프로토타입 메서드로 정의해야 한다.
- 하지마 메서드 내부에서 인스턴스 프로퍼티를 참조할 필요가 없다면 this를 사용하지 않는다.
- this 없이 프로토타입 메서드로 정의하는 방법으로는 인스턴스를 생성한 다음 인스턴스로 호출한다.

→ 클래스 또는 생성자 함수를 하나의 네임스페이스로 사용하여 정적 메서드를 모아 놓아면 이름 충돌 가능성을 줄여 주고 관련 함수들을 구조화할 수 있는 효과가 있다.

이 같은 이유로 정적 메서드는 애플리케이션 전역에서 사용할 유틸리티 함수를 전역 함수로 정의하지 않고 메서드로 구조화할 때 유용하다.

</aside>

### **📌 25.5.5 클래스에서 정의한 메서드의 특징**

<aside>
💵

→ 클래스에서 정의한 메서드는 다음과 같은 특징을 갖는다.

1. function 키워드를 생략한 메서드 축약 표현을 사용한다.
2. 객체 리터럴과는 다르게 클래스 메서드 정의할 때는 콤마가 필요 없다.
3. 암묵적으로 strict mode로 실행된다. 
4. for…in 문이나 Object.keys 메서드 등으로 열거할 수 없다. 즉, 프로퍼티의 열거 가능 여부를 나타내며, 불리언 값을 갖는 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 false다.
5. 내부 메서드 [[Construct]]를 갖지 않는 non-constuctor다. 따라서 new 연산자와 함께 호출할 수 없다.
</aside>

### ⭐️25.6 클래스의 인스턴스 생성 과정

<aside>
💵

→ 클래스의 인스턴스 생성 과정

1. 인스턴스 생성과 this 바인딩
- me 연산자와 함께 클래스를 호출하면 constructor는 암묵적으로 빈 객체가 생성된다.
- 빈 객체는 클래스가 생성한 인스턴스다.
- 빈 객체는 클래스가 생성 한 인스턴스의 프로토타입으로 클래스의 prototype 프로퍼티가 가리키는 객체가 설정된다.
- 빈 객체, 인스턴스는 this에 바인딩된다. 따라서 constructor 내부의 this는 클래스가 생성한 인스턴스를 가리킨다.
1. 인스턴스 초기화
- constructor 내부 코드가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다.
- this에 바인딩되어 있는 인스턴에스 프로퍼티 추가 후 constuctor가 인수로 전달 받은 초기값으로 인스턴스의 프로퍼티 값을 초기화한다.
1. 인스턴스 반환
- 클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

```jsx
class Person {
	// 생성자
	constructor(name) {
		// 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
		console.log(this); // Person {}
		console.log(Object.getPrototypeOf(this) === Person.prototype); // true
		
		// 2. this에 바인딩 되어 있는 인스턴스를 초기화한다.
		this.name = name;
		
		// 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
	}
}
```

</aside>

### ⭐️25.7 프로퍼티

### **📌 25.7.1 인스턴스 프로퍼티**

<aside>
💵

→ 인스턴스 프로퍼티는 constructor 내부에서 정의해야 한다.

- constructor 내부의 this에는 암묵적으로 생성한 인스턴스인 빈 객체가 바인딩되어 있다.
- 클래스가 암묵적으로 생성한 빈 객체, 즉 인스턴스에 프로퍼티가 추가되어 인스턴스가 초기화된다.
- constructor 내부에서 this에 추가한 프로퍼티는 언제가 클래스가 생성한 인스턴스의 프로퍼티가 된다.
</aside>

### **📌 25.7.2 접근자 프로퍼티**

<aside>
💵

→ 접근자 프로퍼티는 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수로 구성된 프로퍼티

- 접근자 프로퍼티는 클래스에서도 사용할 수 있다.
- 접근자 프로퍼티는 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수, getter setter 함수로 구성되어 있다.

→ getter 

- getter는 인스턴스 프로퍼티에 접근할 때마다 프로퍼티 값을 조작하거나 별도의 행위가 필요할 때 사용한다.
- getter는 메서드 이름 앞에 get 키워드를 사용해 정의한다.

→ setter

- setter는 인스턴스 프로퍼티에 값을 할당할 때마다 프로퍼티 값을 조작하거나 별도의 행위가 필요할 때 사용한다.
- setter는 메서드 이름 앞에 set 키워드를 사용해 정의한다.

→ getter, setter 이름은 인스턴스 프로퍼티처럼 사용된다.

- 클래스의 메서드는 기본적으로 프로토타입 메서드가 된다.
- 클래스의 접근자 프로퍼티 또한 인스턴스 프로퍼티가 아닌 프로토타입의 프로퍼티가 된다.
</aside>

### **📌 25.7.3 클래스 필드 정의 제안**

<aside>
💵

→ 클래스 필드란?

- 클래스 기반 객체지향 언어에서 클래스가 생성할 인스턴스의 프로퍼티를 가리키는 용어다.
- 클래스 기반 객체지향 언어인 자바의 클래스 필드는 클래스 내부에서 변수처럼 사용된다.

```jsx
// 자바의 클래스 정의
public class Person {
	// 1 클래스 필드 정의
	// 클래스 필드는 클래스 몸체에 this 없이 선언해야 한다.
	private String firstName = "";
	private String lastName = "";
	
	// 생성자
	Person(String firstName, String lastName){
		// 3. this는 언제나 클래스가 생성할 인스턴스를 가리킨다.
		this.firstName = firstName;
		this.lastName = lastName;
	}
	
	public String getFullName() {
		// 2 클래스 필드 참조ㅓ
		// this 없이도 클래스 필드를 참조할 수 있다.
		return firstName + " " + lastName;
	}
}
```

→ 자바와는 다르게 자바스크립트의 클래스에서 인스턴스 프로퍼티를 선언하고 초기화하려면 반드시 constructor 내부에서 this에 프로퍼티를 추가해야 한다.

- 자바스크립트의 클래스에서 인스턴스 프로퍼티를 참조하려면 반드시 this를 사용하여 참조해야 한다.
- 클래스 기반 객체지향 언어의 this는 언제나 클래스가 생성할 인스턴스를 가리킨다.
- 3과 같이 this는 클래스 필드가 생성자 또는 메서드 매개변수 이름과 동일할 때 클래스 필드임을 명확히 하기 위해 사용한다.
- 자바스크립트의 클래스 몸체에는 메서드만 선언할 수 있다.

→ 클래스 필드 정의 제안은 아직 정식 표준 사양으로 승급되지 않았다.

- 따라서 최신 브라우저와 최신 Node.js에서는 클래스 필드를 클래스 몸체에 정의할 수 있다.
- 클래스 몸체에서 클래스 필드를 정의하는 경우 this에 클래스 필드를 바인딩해서는 안 된다.
- 클래스 필드를 참조하는 경우 자바와 같은 클래스 기반 객체 지향 언어에서는 this를 생략할 수 있으나 자바스크립트에서는 this를 반드시 사용해야 한다.
- 클래스 필드에 초기값을 할당하지 않으면 undefined를 갖는다.
- 인스턴스를 생성할 때 외부의 초기값으로 클래스 필드를 초기화해야 할 필요가 있다면 constructor에서 클래스 필드를 초기화해야 한다.
</aside>

### **📌 25.7.4 private 필드 정의 제안**

<aside>
💵

→ 자바스크립트는 캡슐화를 완전하게 지원하지 않는다.

- 인스턴스 프로퍼티는 인스턴스를 통해 클래스 외부에서 언제나 참조할 수 있다.
- 즉 public으로 되어있다.

```jsx
class Person {

	constructor(name) {
		this.name = name;
	}
}
const me = new Person('Lee');
console.log(me.name); // Lee
```

→ 클래스 필드 정의 제안을 사용하더라도 클래스 필드는 기본적으로 public 하기 때문에 외부에 그대로 노출된다.

```jsx
class Person {
	name = 'Lee'; // 클래스 필드도 기본적으로 public
}

// 인스턴스 생성
const me = new Person();
console.log(me.name); // Lee
```

→ private 필드를 사용해보자

- private 필드의 선두에는 #을 붙여준다.
- private 필드를 참조할 때도 #을 붙여주어야 한다.

```jsx
class Person {
	// private 필드 정의
	#name = '';
	
	constructor(name) {
		// private 필드 참조
		this.name =name;
	}
}

const me = new Person('Lee');

// private 필드 #name은 클래스 외부에서 참조할 수 없다.
console.log(me.#name); // 문법에러
```

| 접근 가능성 | public | private |
| --- | --- | --- |
| 클래스 내부 | o | o |
| 자식 클래스 내부 | o | x |
| 클래스 인스턴스를 통한 접근 | o | x |

→ 이처럼 클래스 외부에서 private 필드에 직접 접근할 수 있는 방법은 없다.
다만 접근자 프로퍼티를 통해 간접적으로 접근하는 방법은 유효하다.

```jsx
get name() {
	// private 필드를 참조하기
	return this.#name.trim()
}
```

→ private 필드는 반드시 클래스 몸체에 정의해야 한다. private 필드를 직접 constructor에 정의하면 에러가 발생한다.

```jsx
class Person{
	constructor(name) {
		// private 필드는 클래스 몸체에서 정의해야 한다.
		this.#name = name;
		// 문법에러
	}
}
```

</aside>

### **📌 25.7.5 static 필드 정의 제안**

<aside>
💵

→ static 키워드로 정적 메서드를 정의할 수 있지만 정적 필드는 정의할 수 없다.

- 새로운 표준 사양 Static public features에서 새롭게 구현되었다.
    1. static class
    2. static private 메서드
    3. static private 필드

```jsx
class MyMath {
	// static public 필드 정의
	static PI = 22 / 7;
	
	// static private 필드 정의
	static #num = 10;
	
	// static 메서드
	static increment() {
		return ++MyMath.#num;
	}
}

console.log(MyMath.PI); // 3.14
console.log(MyMath.increment()); // 11
```

</aside>

### ⭐️25.8 상속에 의한 클래스 확장

### **📌 25.8.1 클래스 상속과 생성자 함수 상속**

<aside>
💵

→ 상속에 의한 클래스 확장은 지금까지 살펴본 프로토타입 기반 상속과는 다른 개념이다.

- 프로토타입 기반 상속은 프로토타입 체인을 통해 다른 객체의 자산을 상속 받는 개념
- 상속에 의한 클래스 확장은 기존 클래스를 상속받아 새로운 클래스를 확장하여 정의하는 것이다.

→ 상속을 구현한 예제를 만들어보자

```jsx
class Animal {
	constructor(age, weight) {
		this.age = age;
		this.weight = weigth;
	}
	
	eat() { return 'eat'; }
	
	move() { return 'move'; }
}

// 상속을 통해 Animal 클래스를 확장한 Bird 클래스
class Bird extends Animal {
	fly() { return 'fly'; }
}

const bird = new Bird(1, 5);

console.log(bird); // Bird {age: 1, weight: 5}
console.log(bird instanceof Bird); // true
console.log(bird instanceof Animal); // true

console.log(bird.eat()); // eat
console.log(bird.move()); // move
console.log(bird.fly()); // fly
```

→ 클래스는 상속을 통해 다른 클래스를 확장할 수 있는 문법인 extends 키워드가 기본적으로 제공된다.

- 생성자 함수는 클래스와 같이 상속을 통해 다른 생성자 함수를 확장할 수 있는 문법이 제공되지 않는다.
- 자바스크립트는 클래스 기반 언어가 아니므로 생성자 함수를 사용하여 클래스를 흉내내는 시도는 권장하지 않지만 의사 클래스 상속 패턴으로 흉내가 가능하다.
- But. 클래스의 등장으로 의사 클래스 상속 패턴은 더이상 사용하지 않는다.
</aside>

### **📌 25.8.2 extends 키워드**

<aside>
💵

→ 상속을 통해 클래스를 확장하려면 extends 키워드를 사용한다.

```jsx
// 부모 클래스
class Base {}

// 자식 클래스
class Derived extends Base{}
```

- 상속을 통해 확장된 클래스를 자식 클래스라 부르고, 상속된 클래스를 부모클래스라 부른다.
- extends 키워드의 역할은 수퍼클래스와 서브클래스 간의 상속 관계를 설정하는 것이다.
- 클래스도 프로토타입을 통해 상속 관계를 구현한다.
- 인스턴스, 클래스 간의 체인을 생성하고, 프로토타입, 정적 메서드 모두 상속이 가능하다.
</aside>

### **📌 25.8.3 동적 상속**

<aside>
💵

→ extends 키워드는 클래스뿐만 아니라 생성자 함수를 상속받아 클래스를 확장할 수도 있다.

- 단 extends 앞에는 반드시 클래스가 와야한다.

```jsx
// 생성자 함수
function Base(a) {
	this.a = a;
}

// 생성자 함수를 상속받는 서브 클래스
class Derived extends Base {}

const derived = new Derived(1);
console.log(derived); // Derived {a: 1}
```

- 조건에 따라 동적으로 상속받을 대상을 결정할 수 있다.

```jsx
function Base1() {}

class Base2 {}

let condition = true;

// 조건에 따라 동적으로 상속 대상을 결정하는 서브클래스
class Derived extends (condition ? Base1 : Base2) {}

const derived = new Derived();
console.log(derived); // Derived {}

console.log(derived instanceof Base1); // true
console.log(derived instanceof Base2); // false
```

</aside>

### **📌 25.8.4 서브클래스의 constructor**

<aside>
💵

→ constructor를 생략시에 클래스에 암묵적으로 정의된다.

서브 클래스에서 constructor를 생략하면 클래스에 다음과 같은 constructor가 암묵적으로 정의된다.

args는 new 연산자와 함께 클래스를 호출할 때 전달한 인수의 리스트다.

→ super()는 수퍼클래스의 constructor(super-constructor)를 호출하여 인스턴스를 생성한다.

`constructor(…args) { super(…args); }`

→ 수퍼클래스와 서브 클래스 모두 constructor를 생략하면 빈 객체가 생성된다.

- 프로퍼티를 소유하는 인스턴스를 생성하려면 construcotr 내부에서 인스턴스에 프로퍼티를 추가해야 한다.
</aside>

### **📌 25.8.5 super 키워드**

<aside>
💵

→ super 키워드는 함수처럼 호출할 수도 있고 this 와 같이 식별자처럼 참조할 수 있는 키워드다.

- super를 호출하면 수퍼클래스의 constructor를 호출한다.
- super를 참조하면 수퍼클래스의 메서드를 호출할 수 있다.

→ super 호출

- 수퍼클래스의 constructor 내부에서 추가한 프로퍼티를 그대로 갖는 인스턴스를 생성한다면 서브클래스의 constructor를 생략할 수 있다.
- 이때 new 연산자와 함께 서브클래스를 호출하면서 전달한 인수는 모두 서브클래스에 암묵적으로 정의된 constructor 의 super 호출을 통해 수퍼클래스의 constructor에 전달된다.

```jsx
// 수퍼클래스
class Base {
	constructor(a,b) {
		this.a = a;
		this.b = b;
	}
}

// 서브 클래스
class Derived extends Base {
	// 암묵적으로 constructor가 정의된다.
}

const derived = new Derived(1, 2);
console.log(derived); // Derived { a:1, b:2 }
```

→ 위와 같이 수퍼클래스에서 추가한 프로퍼티와 서브클래스에서 추가한 프로퍼티를 갖는 인스턴스를 생성하면 서브클래스의 constructor를 생략할 수 없다. 

- 이때 new 연산자와 함께 서브클래스를 호출하면서 전달한 인수 중에서 수퍼클래스의 constructor에 전달할 필요가 있는 인수는 서브클래스의 constructor에서 호출하는 super를 통해 전달한다.

```jsx
// 수퍼클래스
class Base {
	constructor(a,b) { // 4
		this.a = a;
		this.b = b;
	}
}

// 서브 클래스
class Derived extends Base {
	constructor(a, b, c) { // 2
		super(a,b); // 3
		this.c = c;
	}
}

const derived = new Derived(1, 2, 3); // 1
console.log(derived); // Derived { a:1, b:2, c: 3 }
```

→ 부모 클래스에서 정의한 인스턴스 인수들은 자식 클래스의 constructor에 전달되고, super 호출을 통해서 Base 클래스의 constructor에 일부가 전달된다.

→ super를 호출할 때 주의할 사항을 다음과 같다.

1. 서브 클래스에서 constructor를 생략하지 않은 경우 서브클래스의 constructor에서는 반드시 super를 호출해야 한다.

```jsx
class Base {}

class Derived extends Base {
	constructor() {
		// 참조에러
		console.log('constructor all');
	}
}

const derived = new Derived();
```

1. 서브클래스의 constructor 에서 super를 호출하기 전에는 this를 참조할 수 없다.

```jsx
class Base {}

class Derived extends Base {
	constructor() {
		// 참조에러
		
		this.a = 1;
		super();
	}
}

const derived = new Derived(1);
```

1. super는 반드시 서브클래스의 constructor에서만 호출한다. 서브클래스가 아닌 클래스의 constructor나 함수에서 super를 호출하면 에러가 발생한다.

```jsx
class Base {}
	constructor() {
		super(); // 문법에러
	}
}

function Foo() {
	super(); // 문법에러
}
```

→ super 참조

- 메서드 내에서 super를 참조하면 수퍼클래스의 메서드를 호출할 수 있다.
1. 서브클래스의 프로토타입 메서드 내에서 super.sayHi는 수퍼클래스의 프로토타입 메서드 sayHi를 가리킨다.

```jsx
// 수퍼클래스
class Base{
	constructor(name) {
		this.name = name;
	}
	
	sayHi() {
		return `Hi ${this.name}`;
	}
}

// 서브 클래스 
class Derived extends Base {
	sayHi() {
		// super.sayHi는 수퍼클래스의 프로토타입 메서드를 가리킨다.
		return `${super.sayHi()}. how are you doing?`;
	}
}

const derived = new Derived('Lee');
console.log(derived.sayHi()); // Hi Lee. how are you doing?
```

 → 수퍼클래스의 sayHi 메서드를 호출할 때는 call 메서드를 사용해 this를 전달해야한다.

- call 없이 sayHi를 호출하게 된다면, sayHi 메서드 내부의 this는 서브 클래스의 prototype을 가리킨다.

→ ES6 메서드 축약으로 super 프로토타입 메서드 불러오기

```jsx
const base = {
	name: 'Lee',
	sayHi() {
		return `Hi! ${this.name}`;
	}
};

const derived = {
	__proto__ : base,
	// ES6 메서드 축약 표현으로 정의한 메서드로, [[HomeObject]]를 갖는다.
	sayHi() {
		return `${super.sayHi()}. how are you doing`;
	}
};

console.log(derived.sayHi()); // Hi! Lee. how are you doing
```

1. 서브클래스의 정적 메서드 내에서 super.sayHi는 수퍼클래스의 정적 메서드 sayHi를 가리킨다.

```jsx
// 수퍼클래스
class Base {
	static sayHi(){
		return 'Hi';
	}
}

// 서브클래스
class Derived extends Base {
	static sayHi() {
		// super.sayHi는 수퍼클래스의 정적 메서드를 가리킨다.
		return `${super.sayHi()} how are you doing?`;
	}
}

console.log(Derived.sayHi()); // Hi how are you doing?
```

</aside>

### **📌 25.8.6 상속 클래스의 인스턴스 생성 과정**

<aside>
💵

→ 상속 관계에 있는 두 클래스의 인스턴스 생성 과정을 확인해보자

```jsx
// 수퍼클래스
class Rectangle {
	constructor(width, height) {
		this.width = width;
		this.height = height;
	}
	
	getArea() {
		return this.width * this.height;
	}
	
	toString() {
		return `width = ${this.width}, height = ${this.height}`;
	}
}

// 서브클래스
class ColorRectangle extends Rectangle {
	constructor(width, height, color) {
		super(width, height);
		this.color = color;
	}
	
	// 메서드 오버라이딩
	toString() {
		return super.toString() + `, color = ${this.color}`;
	}
}

const colorRectangle = new ColorRectangle(2, 4, 'red');
console.log(colorRectangle); // ColorRectangle { width: 2, height: 4, color: 'red'}

// 상속을 통해 getArea 메서드 호출
console.log(colorRectangle.getArea()); // 8
// 오버라이딩 toString 메서드 호출
console.log(colorRectangle.toString()); // width = 2, height = 4, color = red
```

→ 서브클래스 ColorRectangle이 new 연산자와 함께 호출되면 다음 과정을 통해 인스턴스를 생성한다.

1. 서브클래스의 super 호출

- 자바스크립트 엔진은 클래스를 평가할 때 수퍼클래스와 서브클래스를 구분하기 위해 값으로 갖는 내부 슬롯 [[ConstructorKid]]를 갖는다.
- 상속받지 않는 클래스는 [[ConstructorKid] 값이 “base” 상속받는 서브클래스는  [[ConstructorKid] 값이 “derived”로 설정된다.
- 이를 통해 수퍼클래스와 서브클래스는 new 연산자와 함께 호출되었을 때의 동작이 구분된다.

→ 서브 클래스는 암묵적으로 빈 객체, 인스턴스를 생성하지 않고 수퍼클래스에게 인스턴스 생성을 위임한다.

- 이것이 바로 서브 클래스의 constructor에서 반드시 super를 호출해야 하는 이유다.
- 서브 클래스가 new 연산자와 함께 호출되면 서브클래스 내부의 super 키워드가 함수처럼 호출된다.
- 만약 서브클래스 constructor 내부에 super 호출이 없으면 에러가 발생한다. →실제로 인스턴스를 생성하는 주체는 수퍼클래스이므로 수퍼클래스의 constructor를 호출하는 super가 호출되지 않으면 인스턴스를 생성할 수 없다,

2. 수퍼클래스의 인스턴스 생성과 this 바인딩

- 수퍼클래스의 constructor 내부의 코드가 실행되기 이전에 암묵적으로 빈 객체를 생성한다.
- 빈 객체가 바로 클래스가 생성한 인스턴스다.
- 암묵적으로 생성된 빈 객체, 인스턴스는 this에 바인딩되고, 수퍼클래스의 constructor 내부의 this는 생성된 인스턴스를 가리킨다.

```jsx
// 수퍼클래스
	class Rectangle {
		constructor(width, height) {
		// 암묵적으로 빈 객체, 인스턴스가 생성되고 this에 바인딩된다.
		console.log(this); // ColorRectangle {}
		// new 연산자와 함께 호출된 함수, 즉 new.target은 ColorRectangle이다.
		console.log(new.target); // ColorRectangle
```

→ 인스턴스는 수퍼클래스가 생성한 것이다.

- new 연산자와 함께 호출된 클래스가 서브클래스라는 것이 중요하다.
- new 연산자와 함께 호출된 함수를 가리키는 new.target은 서브클래스를 가리킨다.
- 따라서 인스턴스를 new.target이 가리키는 서브클래스가 생성한 것으로 처리된다.

```jsx
// 수퍼클래스
class Rectangle {
	constructor(width, height) {
		// 암묵적으로 빈 객체, 즉 인스턴스 생성되고 this에 바인딩된다.
		console.log(this); // ColorRectangle {}
		// new 연산자와 함께 호출된 함수, new.target은 ColorRectangle이다.
		console.log(new.target); // ColorRectangle
		
		// 생성된 인스턴스의 프로토타입으로 ColorRectangle.prototype이 설정된다.
		console.log(Object.getPrototypeOf(this) === ColorRectangle.prototype);// true
		console.log(this instanceof ColorRectangle); // true
		console.log(this instanceof Rectangle); // true
```

3. 수퍼클래스의 인스턴스 초기화

→ 수퍼클래스의 constructor가 실행되어 this가 바인딩되어 있는 인스턴스를 초기화한다.

- this에 바인딩 되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티를 초기화한다.

```jsx
// 수퍼클래스
class Rectangle {
	constructor(width, height) {
		// 암묵적으로 빈 객체, 즉 인스턴스가 생성되고 this에 바인딩
		console.log(this); // ColorRectangle {}
		// new 연산자와 함께 호출된 함수, new.target은 ColorRectangle이다.
		console.log(new.target); // ColorRectangle
		
		// 생성된 인스턴스의 프로토타입으로 ColorRectangle.prototype이 설정된다.
		console.log(Object.getPrototypeOf(this) === ColorRectangle.prototype); // true
		console.log(this instanceof ColorRectangle); // true
		console.log(this instanceof Rectangle); // true
		
		// 인스턴스 초기화
		this.width = width;
		this.height = height;
		
		console.log(this); // ColorRectangle {width: 2, height: 4}
```

4. 서브 클래스 constructor로의 복귀와 this 바인딩

→ super 호출 종료 후 제어 흐름이 서브클래스 constructor로 돌아온다.

- super가 반환한 인스턴스가 this에 바인딩된다.
- 서브 클래스는 별도의 인스턴스 생성 x, super가 반환한 인스턴스를 this에 바인딩하여 그대로 사용한다.

```jsx
// 서브클래스
class ColorRectangle extends Rectangle {
	constructor(width, height, color) {
		super(width, height);
		
		// super가 반환한 인스턴스가 this에 바인딩된다.
		console.log(this); // ColorRectangle {width: 2, height: 4}
```

→ super가 호출되지 않으면 인스턴스가 생성되지 않는다.

- this 바인딩도 불가능이다.
- 서브클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없는 이유가 이것 때문이다.

5. 서브클래스의 인스턴스 초기화

- super 호출 이후 서브클래스의 constructor에 기술되어 있는 인스턴스 초기화가 실행된다.
- this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티를 초기화한다.

6. 인스턴스 반환

→ 클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

</aside>

### **📌 25.8.7 표준 빌트인 생성자 함수 확장**

<aside>
💵

→ extends 키워드 다음에는 클래스 뿐만 아니라 [[Construct]] 내부 메서드를 갖는 함수 객체로 평가될 수 있는 모든 표현식을 사용할 수 있다.

- 따라서 표준 빌트인 객체도 extends 키워드를 사용하여 확장할 수 있다.
</aside>