### ⭐️20.1 strict mode란?

<aside>
🧞

```jsx
function foo() {
	x = 10;
}
foo();

console.log(x); // ?
```

→ foo 함수 내 선언하지 않은 x 변수에 값 10을 할당, 이때 엔진은 x 변수를 찾기 위해 스코프 체인을 통해 검색을 시작한다.

1. 엔진은 foo 함수의 스코프 내에서 x 변수를 검색한다. → 없음
2. 엔진은 foo 함수 컨텍스트의 상위 스코프에서 x 변수의 선언을 검색한다. → 있음

→ ? 왜 선언 안했는데?

- 엔진은 암묵적으로 전역 객체에 x 프로퍼티를 동적 생성한다.
- 이때 전역 객체의 x 프로퍼티는 마치 전역 변수처럼 사용할 수 있다.
- 이런 현상을 암묵적 전역이라 한다.

→ 개발자 의도와는 상관없이 발생한 암묵적 전역은 오류를 발생시키는 원인이 크다.

- 이러한 잠재적인 오류를 발생시키는 환경을 최소화 시키는 것이 ES5 부터 추가된 strict mode(엄격 모드) 이다.
- ESLint 같은 린트 도구를 사용해도 strict mode 와 유사한 효과를 얻을 수 있다.
- 린트 도구는 strict mode가 제한하는 오류는 물론 코딩 컨벤션을 설정 파일 형태로 정의하고 강제할 수 있기 때문에 더욱 강력한 효과를 얻을 수 있다.
</aside>

### ⭐️20.2 strict mode의 적용

<aside>
🧞‍♂️

→ strict mode를 적용하기 위해서는 전역의 선두 또는 함수 몸체의 선두에 `“use strict”;` 를 추가한다.

- 전역의 선두에 추가하면 스크립트 전체에 strict mode가 적용된다.

```jsx
// 올바른 적용 (전역에 추가)
'use strict';
function foo() {
	x = 10; // 참조 에러 (스트릭트 모드)
}
foo() 

// 올바른 적용 (함수 몸체에 추가)
function foo() {
	'use strict';
	x = 10; // 참조 에러(스트릭트 모드)
}

// 잘못된 적용
function foo() {
	x = 10; // 에러 발생 안함
	'use strict';
}
foo();
```

</aside>

### ⭐️20.3 전역에 strict mode를 적용하는 것은 피하자

<aside>
🧞‍♀️

→ 전역에 적용한 strict mode 는 스크립트 단위로 적용된다.

But. strict mode 스크립트와 non-strict mode 스크립트를 혼용하는 것은 오류를 발생시킬 수 있다.

- 외부 서드파티 라이브러리를 사용하는 경우 라이브러리가 non-strict mode인 경우도 있기 때문에 전역에 strict mode를 적용하는 것은 바람직하지 않다.
- 이러한 경우 즉시 실행 함수로 스크립트 전체를 감싸서 스코프를 구분하고 즉시 실행 함수의 선두에 strict mode를 적용한다.

```jsx
// 즉시 실행 함수의 선두에 strict mode 적용
(function () {
	'use strict';
	
	// Do something...
}());
```

</aside>

### ⭐️20.4 함수 단위로 strict mode를 적용하는 것도 피하자

<aside>
🧜

→ 함수 단위로 strict mode를 적용할 수도 있다.

- 그러나 각 함수마다 서로다르게 strict mode를 적용하는것은 올바르지 않다.
- 또한 번거롭게 함수마다 설정하는 것도 귀찮다..
- 따라서 strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직하다.
</aside>

### ⭐️20.5 strict mode가 발생시키는 에러

→ 다음은 strict mode를 적용했을 때 에러가 발생하는 대표적인 사례들이다.

### **📌 20.5.1 암묵적 전역**

<aside>
🤼

→ 선언하지 않은 변수를 참조하면 ReferenceError 가 발생한다.

```jsx
(function() {
	'use strict';
	
	x = 1;
	console.log(x); // 참조에러
}());
```

</aside>

### **📌 20.5.2 변수, 함수, 매개변수의 삭제**

<aside>
🐕‍🦺

→ delete 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxError가 발생한다.

```jsx
(function ( ){
	'use strict';
	
	var x = 1;
	delete x; // SyntaxError
	
	function foo(a) {
		delete a; // SyntaxError
	}
	delete foo; // SyntaxError
}());
```

</aside>

### **📌 20.5.3 매개변수 이름의 중복**

<aside>
🐕

→ 중복된 매개변수 이름을 사용하면 SyntaxError가 발생한다.

```jsx
(function () {
	'use strict';
	
	// SyntaxError
	function foo(x, x) {
		return x + x;
	}
	console.log(foo(1,2));
}());
```

</aside>

### **📌 20.5.4 with 문의 사용**

<aside>
🐺

→ with 문을 사용하면 SyntaxError가 발생한다.

- with 문은 전달된 개겣를 스코프 체인에 추가한다.
- with문은 동일한 객체의  프로퍼티를 반복해서 사용할 때 객체 이름을 생략할 수 있어서 코드가 간단해지는 효과가 있다.
- 하지만 성능과 가독성이 나빠지는 문제가 있다.

```jsx
(function () {
	'use strict';
	
	// SyntaxError
	with({ x: 1 }) {
		console.log(x);
	}
}());
```

</aside>

### ⭐️20.6 strict mode 적용에 의한 변화

### **📌 20.6.1 일반 함수의 this**

<aside>
🐛

→ strict mode 에서 함수르 일반 함수로서 호출하면 this에 undefined가 바인딩된다.

- 생성자 함수가 아닌 일반 함수 내부에서는 this를 사용할 필요가 없기 때문이다. → 에러는 발생하지 않는다.

```jsx
(function () {
	'use strict';
	
	function foo() {
		console.log(this); // undefined
	}
	foo();
	
	function Foo() {
		console.log(this); // Foo
	}
	new Foo();
}());
```

</aside>

### **📌 20.6.2 arguments 객체**

<aside>
🦌

→ strict mode 에서는 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않는다.

```jsx
(function (a) {
	'use strict';
	// 매개변수에 전달된 인수를 재할당하여 변경
	a = 2;
	
	// 변경된 인수가 arguments 객체에 반영되지 않는다.
	console.log(arguments); // { 0: 1, length: 1 }
}(1));
```

</aside>