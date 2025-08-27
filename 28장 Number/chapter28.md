### ⭐️28.1 Number 생성자 함수

<aside>
🔕

→ 표준 빌트인 객체인 Number 객체는 생성자 함수 객체다.

- 생성자 함수 객체는 new 연산자와 함께 호출하여 인스턴스를 생성한다.
- 생성자 함수 호출 시 인수를 전달하지 않으면 0이 담긴체 객체가 생성된다.
- Number 생성자 함수의 인수로 숫자가 아닌 값을 전달하면 숫자로 강제 변환한다.

```jsx
const numObj = new Number();
console.log(numObj); // Number {[[PrimitiveValue]]: 0}

const numObj = new Number(10);
console.log(numObj); // Number {[[PrimitiveValue]]: 10}

let numObj = new Number('10');
console.log(numObj); // Number {[[PrimitiveValue]]: NaN}

numObj = new Number('Hello');
console.log(numObj); // Number {[[PrimitiveValue]]: NaN}

// 문자열 타입 => 숫자 타입
Number('0'); // -> 0
Number('-1'); // -> -1
Number('10.53'); // -> 10.53

// 불리언 타입 => 숫자 타입
Number(true); // -> 1
Number(false); // -> 0
```

</aside>

### ⭐️28.2 Number 프로퍼티

### **📌 28.2.1 Number.EPSILON**

<aside>
🔕

→ ES6에서 도입된 Number.EPSILON은 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이와 같다.

- 부동소수점 산술 연산은 정확한 결과를 기대하기 어렵다.
- 정수는 2진법으로 오차없이 저장 가능하지만 IEEE 754는 2진법으로 변환했을 때 무한소수가 되어 미세한 오차를 발생한다.

```jsx
0.1 + 0.2; // -> 0.300000000000000004
0.1 + 0.2 === 0.3; // -> false

// 이때 사용하는것이 Number.EPSILON
function isEqual(a, b) {
	// a와 b를 뺀 값의 절대값이 Number.EPSILON보다 작으면 같은 수로 인정
	return Math.abs(a - b) < Number.EPSILON;
}
isEqual(0.1 + 0.2, 0.3) // -> true
```

</aside>

### **📌 28.2.2 Number.MAX_VALUE**

<aside>
🔕

→ Number.MAX_VALUE는 자바스크립트에서 표현할 수 있는 가장 큰 양수이다.

- Number.MAX_VALUE보다 큰 숫자는 Infinity다.

```jsx
Number.MAX_VALUE; 
Infinity > Number.MAX_VALUE; // -> true
```

</aside>

### **📌 28.2.3 Number.MIN_VALUE**

<aside>
🔕

→ Number.MIN_VALUE는 자바스크립트에서 표현할 수 있는 가장 작은 양수 값이다.

- Number.MIN_VALUE보다 작은 숫자는 0이다.

```jsx
Number.MIN_VALUE;
Number.MIN_VALUE > 0; // -> true
```

</aside>

### **📌 28.2.4 Number.MAX_SAFE_INTEGER**

<aside>
🔕

→ Number.MAX_SAFE_INTEGER는 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수 값이다.

`Number.MAX_SAFE_INTEGER;` 

</aside>

### **📌 28.2.5 Number.MIN_SAFE_INTEGER**

<aside>
🔕

→ Number.MIN_SAFE_INTEGER는 자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수 값이다.

`Number.MIN_SAFE_INTEGER`

</aside>

### **📌 28.2.6 Number.POSITIVE_INFINITY**

<aside>
🔕

→ Number.POSITIVE_INFINITY는 양의 무한대를 나타내는 숫자값 Infinity 와 같다.

**`Number.POSITIVE_INFINITY`**

</aside>

### **📌 28.2.7 Number.NEGATIVE_INFINITY**

<aside>
🔕

→ Number.POSITIVE_INFINITY는 음의 무한대를 나타내는 숫자값 -Infinity 와 같다.

**`Number.NEGATIVE_INFINITY`**

</aside>

### **📌 28.2.8 Number.NaN**

<aside>
🔕

→ Number.NaN은 숫자가 아님(Not-a-Number)을 나타내는 숫자값이다.

- Number.NaN은 window.NaN과 같다.

`Number.NaN` 

</aside>

### ⭐️28.3 Number 메서드

### **📌 28.3.1 Number.isFinite**

<aside>
🔕

→ ES6에서 도입된 Number.isFinite 정적 메서드는 인수로 전달된 숫자값이 정상적인 유한수, 즉 Infinity인지 -Infinity 가 아닌지 검사하여 결과를 불리언 값으로 반환한다.

```jsx
// 인수가 정상적인 유한수이면 true를 반환한다.
Number.isFinite(0); // -> true
Number.isFinite(Number.MAX_VALUE); // -> true
Number.isFinite(Number.MIN_VALUE); // -> true

// 인수가 무한수이면 false로 반환한다.
Number.isFinite(Infinity); // -> false
Number.isFinite(-Infinity); // -> false

// 인수가 NaN이면 언제나 false를 반환한다.
Number.isFinite(NaN); // -> false

// Number.isFinite는 인수를 숫자로 암묵적 타입 변환하지 않는다.
Number.isFinite(null); // -> false
// isFinite는 인수를 숫자로 암묵적 타입 변환한다. null은 암묵적으로 0
isFinite(null); // -> true
```

</aside>

### **📌 28.3.2 Number.isInteger**

<aside>
🔕

→ ES6에서 도입된 Number.isInteger 정적 메서드는 인수로 전달된 숫자값이 정수인지 검사하여 그 결과를 불리언 값으로 반환한다.

- 검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다.

```jsx
// 인수가 정수이면 true를 반환한다.
Number.isInteger(0) // -> true
Number.isInteger(123) // -> true
Number.isInteger(-123) // -> true

// 0.5는 정수가 아니다.
Number.isInteger(0.5) // -> false
// '123'을 숫자로 암묵적 타입 변환하지 않는다.
Number.isInteger('123') // -> false
// false를 숫자로 암묵적 타입 변환하지 않는다.
Number.isInteger(false) // -> false
Number.isInteger(Infinity) // -> false
Number.isInteger(-Inifinity) // -> false
```

</aside>

### **📌 28.3.3 Number.isNaN**

<aside>
🔕

→ ES6에서 도입된 Number.isNaN 정적 메서드는 인수로 전달된 숫자값이 NaN인지 검사하여 그 결과를 불리언 값으로 반환한다.

```jsx
// 인수가 NaN이면 true를 반환한다.
Number.isNaN(NaN); // -> true

// Number.isNaN 메서드는 isNaN과 차이가 있다.
// 암묵적 타입 변환에 따른 다른점.
// Number.isNaN은 인수를 숫자로 암묵적 타입 변환하지 않는다.
Number.isNaN(undefined); // -> false
// isFinite는 인수를 숫자로 암묵적 타입 변환 한다.
isNaN(undefined); // -> true
```

</aside>

### **📌 28.3.4 Number.isSafeInteger**

<aside>
🔕

→ ES6에서 도입된 Number.isSafeInteger 정적 메서드는 인수로 전달된 숫자값이 안전한 정수인지 검사하여 그 결과를 불리언 값으로 반환한다.

- 안전한 정수값은 -(253-1) 과 253 - 1 사이의 정수값이다.

```jsx
// 0은 안전한 정수다.
Number.isSafeInteger(0); // -> true
// 1000000000은 안전한 정수다.
Number.isSafeInteger(1000000000000); // -> true
// 1000000000001은 안전하지 않다.
Number.isSafeInteger(1000000000000001); // -> false
// 0.5는 정수가 아니다.
Number.isSafeInteger(0.5); // -> false
// '123'을 숫자로 암묵적 타입 변환하지 않는다.
Number.isSafeInteger('123'); // -> false
// false를 숫자로 암묵적 타입 변환하지 않는다.
Number.isSafeInteger(false); // -> false
// Infinity/ -Infinity는 정수가 아니다.
Number.isSafeInteger(Infinity); // -> false
```

</aside>

### **📌 28.3.5 Number.prototype.toExponential**

<aside>
🔕

→ toExponential 메서드는 숫자를 지수 표기법으로 변환하여 문자열로 반환한다.

- 지수 표기법이란매우 크거나 작은 숫자를 표기할 때 사용하며 e 앞에 숫자에 10의 n승을 곱하는 형식으로 수를 나타낸다.

```jsx
(77.1234).toExponential(); // -> '7.71234e+1'
(77.1234).toExponential(4); // -> '7.7123e+1'

// 숫자 리터럴과 함께 사용할 경우 에러가 발생한다.
77.toExponential(); // -> SyntaxError
```

</aside>

### **📌 28.3.6 Number.prototype.toFixed**

<aside>
🔕

→ toFixed 메서드는 숫자를 반올림하여 문자열로 반환한다.

- 반올림하는 소수점 이하 자릿수를 나타내는 0 ~ 20 사이의 정수값을 인수로 전달할 수 있다.
- 인수를 생략하면 기본값 0 이 지정된다.

```jsx
// 소수점 이하 반올림. 인수를 생략하면 기본값 0이 지정한다.
(12345.6789).toFixed(); // "12345"
// 소수점 이하 1자리수 유효 나머지 반올림
(12345.6789).toFixed(1); // "12345.6"
```

</aside>

### **📌 28.3.7 Number.prototype.toPrecision**

<aside>
🔕

→ toPrecision 메서드는 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다.

```jsx
(12345.6789).toPrecision(); // -> "12345.6789"
// 전체 1자릿수 유효
(12345.6789).toPrecision(1); // -> "1e+4"
// 전체 2자릴수 유효
(12345.6789).toPrecision(2); // -> "1.2e+4"
```

</aside>

### **📌 28.3.8 Number.prototype.toString**

<aside>
🔕

→ toString 메서드는 숫자를 문자열로 변환하여 반환한다.

- 진법을 나타내는 2 ~ 36 사이의 정수값을 인수로 전달할 수 있다.
- 인수를 생략하면 기본값 10진법이 지정된다.

```jsx
// 인수를 생략하면 10진수 문자열이 반환한다.
(10).toString(); // "10"
// 2진수 문자열을 반환한다.
(16).toString(2); // -> "10000"
```

</aside>