### ⭐️타입 변환이란?

- 자바스크립트의 모든 값은 타입이 있다.
- 개발자가 의도적으로 값의 타입을 변환하는 것을 **명시적 타입 변환** 또는 **타입 캐스팅**이라 한다.

```jsx
var x = 10;

// 명시적 타입 변환
// 숫자를 문저열로 타입 캐스티한다.
var str = x.toString();
console.log(typeof str, str); // string 10

// x 변수의 값이 변경된 것은 아니다.
console.log(typeof x, x); // number 10
```

- 개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입 변환이 되기도 한다.
- 이를 **암묵적 타입 변환** 또는 **타입 강제 변환**이라 한다.

```jsx
var x = 10;

// 암묵적 타입 변환
// 문자열 연결 연산자는 숫자 타입 x의 값을 바탕으로 새로운 문자열을 생성한다.
var str = x + "";
console.log(typeof str, str); // string 10

// x 변수의 값이 변경된 것은 아니다.
console.log(typeof x, x); // number 10
```

→ 명시적 타입 변환이나 암묵적 타입 변환이 기존 원시 값(x)을 직접 변경하는 것은 아니다.

- 원시 값은 변경 불가능한 값 이므로 , 타입 변환은 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성한다.

→ 암묵적 타입 변환은 기존 변수 값을 재할당 하여 변경하는 것이 아니다.

- 자바스크립트 엔진은 표현식을 에러 없이 평가하기 위해 값을 암묵적 타입 변환 후 새로운 값 생성 후 단 한번 사용하고 버린다.

→ 암묵적 타입 변환은 개발자의 의도가 드러나지 않기에, 오류를 생성할 확률이 높아진다!

### ⭐️암묵적 타입 변환

- 자바스크립트 엔진은 표현식을 평가할 때 개발자의 의도와는 상관없이 코드의 문맥을 고려하여 암묵적으로 데이터 타입을 강제 변환한다.

```jsx
// 피연산자가 모두 문자열 타입이어야 하는 문맵
"10" + 2; // -> '102'

// 피연산자가 모두 숫자 타입이어야 하는 문맥
5 * "10"; // -> 50

// 피연산자 또는 표현식이 불리언 타입이어야 하는 문맥
!0; // -> true
if (1) {
}

// 암묵적 타입 변환이 발생하면 문자열, 숫자, 불리언과 같은 원시 타입 중 하나로 타입을 자동 변환한다.
```

### **📌 문자열 타입으로 변환**

`1 + ‘2’  = ‘12’` ← + 연산자는 피연산자 중 하나 이상이 문자열이므로 문자열 연결 연산자로 동작한다.

→ 자바스크립트 엔진이 암묵적 타입 변환을 수행할 때 동작하는 방식

```jsx
// 숫자타입
0 + '' // -> "0"
-0 + '' // -> "0"
1 + '' // -> "1"
-1 + '' // -> "-1"
NaN + '' // -> "NaN"
Infinity + '' // -> "Infinity"
-Infinity + '' // -> "-Infinity"

// 불리언 타입
true + '' // -> "true"
false + '' // -> "false"

// null 타입
null + '' // -> "null"

// undefined 타입
undefined + '' // -> "undefined"

// 심벌 타입
(Symbol()) + '' // -> Type Error

//객체 타입
({}) + '' // -> "[object object]"
Math + '' // -> "[object Math]"
[] + ''  // -> ""
[10, 20] + '' // -> "10, 20"
(function(){}) + '' // -> "function(){}"
Array + '' // -> "function Array() { [native code] }"
```

### **📌 숫자 타입으로 변환**

- 산술 연산자의 모든 피연산자는 코드 문맥상 모두 숫자 타입이여야 한다.
- 이때 피연산자를 숫자 타입으로 변환할 수 없는 경우에는 산술 연산을 수행 할 수 없으므로 NaN 이 된다.

→ 자바스크립트 엔진이 암묵적 타입 변환을 수행할 때 동작하는 방식

```jsx
// 문자열 타입
+"" + // -> 0
  "0" + // -> 0
  "1" + // -> 1
  "string" + // -> NaN
  // 불리언 타입
  true + // -> 1
  false + // -> 0
  // null 타입
  null + // -> 0
  // undefined 타입
  undefined + // -> NaN
  // 심벌 타입
  Symbol() + // -> TypeError
  //객체 타입
  {} + // -> NaN
  [] + // -> 0
  [10, 20] + // -> NaN
  function () {}; // -> NaN
```

### **📌 불리언 타입으로 변환**

- `if (’’) console.log(x);` → 제어문 또는 삼항 조건 연산자의 조건식은 불리언 값.
- 자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입 변환 한다.

```jsx
if ("") console, log("1");
if (true) console, log("2");
if (0) console, log("3");
if ("str") console, log("4");
if (null) console, log("5");

// 2 4
```

- 이때 자바스크립트 엔진 불리언 타입이 아닌 값을 Truthy 값 ( 참으로 평가되는 값) 또는 Falsy 값 (거짓으로 평가되는 값) 으로 구분한다.

→ false 로 평가되는 Falsy 값

```jsx
// 아래의 조건문은 모두 코드 블록을 실행한다.
if (!false) console, log(false + " is falsy value");
if (!undefined) console, log(undefined + " is falsy value");
if (!null) console, log(null + " is falsy value");
if (!0) console, log(0 + " is falsy value");
if (!NaN) console, log(NaN + " is falsy value");
if (!"") console, log("" + " is falsy value");
```

→ Truthy/Falsy 값을 판별 하는 함수

```jsx
function isFalsy(v) {
  return !v;
}
function isTruthy(v) {
  return !v;
}
```

### ⭐️명시적 타입 변환

→ 명시적으로 타입을 변경하는 방법

- 표준 빌트인 생성자 함수를 new 연산자 없이 호출하는 방법
- 빌트인 메서드를 사용하는 방법
- 암묵적 타입 변환을 이용하는 방법

### ⭐️명시적 타입 변환

→ 명시적으로 타입을 변경하는 방법

- 표준 빌트인 생성자 함수를 new 연산자 없이 호출하는 방법
- 빌트인 메서드를 사용하는 방법
- 암묵적 타입 변환을 이용하는 방법

### **📌 문자열 타입으로 변환**

→ 문자열 타입이 아닌 값을 문자열 타입으로 변환하는 방법

- String 생성자 함수를 new 연산자 없이 호출하는 방법
- Object.prototype.toString 메서드를 사용하는 방법
- 문자열 연결 연산자를 이용하는 방법

```jsx
// 1. String 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 => 문자열 타입
String(1); // -> "1"
String(NaN); // -> "NaN"
String(Infinity); // -> "Infinity"
// 불리언 타입 => 문자열 타입
String(true); // -> "true"
String(false); // -> "false"

// 2. Object.prototype.toString 메서드를 사용하는 방법
// 숫자 타입 => 문자열 타입
(1).toString(); // -> "1"
NaN.toString(); // -> "NaN"
Infinity.toString(); // -> "Infinity"
// 불리언 타입 => 문자열 타입
true.toString(); // -> "true"
false.toString(); // -> "false"

// 3. 문자열 연결 연산자를 이용하는 방법
// 숫자 타입 => 문자열 타입
1 + ""; // -> "1"
NaN + ""; // -> "NaN"
Infinity + ""; // -> "Infinity"
// 불리언 타입 => 문자열 타입
true + ""; // -> "true"
false + ""; // -> "false"
```

### **📌 숫자 타입으로 변환**

→ 숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법

- Number 생성자 함수를 new 연산자 없이 호출하는 방법
- paserInt. parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
- - 단항 산술 연산자를 이용하는 방법
- - 산술 연산자를 이용하는 방법

```jsx
// 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 숫자 타입
Number("0"); // -> 0
Number("-1"); // -> -1
Number("10.53"); // -> 10.53
// 불리언 타입 => 숫자 타입
Number(true); // -> 1
Number(false); // -> 0

// 2. paserInt. parseFloat 함수를 사용하는 방법(문자열만 변환 가능)
// 문자열 타입 => 숫자 타입
parseInt("0"); // -> 0
parseInt("-1"); // -> -1
parseInt("10.53"); // -> 10.53

// 3. + 단항 산술 연산자를 이용하는 방법
+"0"; // -> 0
+"-1"; // -> -1
+"10.53"; // -> 10.53
+true + // -> 1
  false; // -> 0

// 4. * 산술 연산자를 이용하는 방법
"0" * 1; // -> 0
"-1" * 1; // -> -1
"10.53" * 1; // -> 10.53
true * 1; // -> 1
false * 1; // -> 0
```

### **📌 불리언 타입으로 변환**

→ 불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법

- Boolean 생성자 함수를 enw 연산자 없이 호출하는 방법
- ! 부정 논리 연산자를 두 번 사용하는 방법

```jsx
Boolean("x"); // -> true
Boolean(""); // -> false
Boolean("false"); // -> true
Boolean(0); // -> false
Boolean(1); // -> true
Boolean(NaN); // -> false
Boolean(Infinity); // -> true
Boolean(null); // -> false
Boolean(undefined); // -> false
Boolean({}); // -> true
Boolean([]); // -> true

!!"x"; // -> true
!!""; // -> false
!!"false"; // -> true
!!0; // -> false
!!1; // -> true
!!NaN; // -> false
!!Infinity; // -> true
!!null; // -> false
!!undefined; // -> false
!!{}; // -> true
!![]; // -> true
```

### ⭐️단축 평가

### **📌 논리 연산자를 사용한 단축 평가**

```jsx
'Cat' && 'Dog' // → 'Dog'
'Cat' || 'Dog' // → 'Cat'
false || 'Dog' // → 'Dog'
'Cat' || false // → 'Cat'
'Cat' && 'Dog' // → 'Dog'
false && 'Dog' // → false
'Cat' && 'false // → false
```

| 단축 평가 표현식    | 평가 결과 |
| ------------------- | --------- |
| true \|\| anything  | true      |
| false \|\| anything | anything  |
| true && anything    | anything  |
| false && anything   | false     |

```jsx
var done = true;
var message = "";

if (done) message = "완료";
if (!done) message = "미완료";

message = done && "완료";
console.log(message); // 완료
message = done || "미완료";
console.log(message); // 미완료

message = done ? "완료" : "미완료";
console.log(message); // 완료
```

```jsx
var elem = null;
var value = elem?.value;
console.log(value); // undefined

var value = elem && elem.value;
console.log(value); // null
```

```jsx
var str = "";
var length = str && str.length;
console.log(length); // ''

var length = str?.length;
console.log(length); // 0
```

```jsx
var foo = null ?? "default string";
console.log(foo); // "default string"

var foo = "" || "default string";
console.log(foo); // "default string"

var foo = "" ?? "default string";
console.log(foo); // ''
```
