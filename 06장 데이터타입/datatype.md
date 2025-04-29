- 데이터 타입은 값의 종류를 말한다.
- 자바스크립트는(ES6) 7개의 데이터 타입을 제공한다. 7개의 데이터 타입은 원시타입과 같은 객체 타입으로 분류할 수 있다.

| 구분 | 데이터 타입 | 설명 |
| --- | --- | --- |
| **원시 타입** | `String` | 문자열, 텍스트 데이터 (`"hello"`, `'world'`) |
|  | `Number` | 숫자 (정수, 부동소수점 모두 포함. `1`, `3.14`) |
|  | `Boolean` | 논리값 (`true`, `false`) |
|  | `undefined` | 값이 할당되지 않은 변수의 초기 상태 (`let x;`) |
|  | `null` | 명시적으로 "값 없음"을 나타내는 값 (`let x = null;`) |
|  | `Symbol` | 유일한 식별자를 만들 때 사용 (`Symbol('id')`) |
| **객체 타입** | `Object` | 여러 값을 키-값 쌍으로 저장 (`{ name: "Yubin", age: 20 }`) |

- 숫자 타입 1 과 문자열 타입 ‘1’ 은 비슷해 보이지만 메모리 공간도 다르고 읽혀 들어오는 해석도 다르다!

### ⭐️숫자타입

- 자바스크립트는 독특하게 하나의 숫자 타입만 존재한다.
- ECMAScript 사양에 따르면 숫자 타입의 값은 배정밀도(64비트) 형식의 2진수로 저장된다.

```jsx
var integer = 10; // 정수
var double = 10.12; // 실수
var negative = -20; // 음의 정수
var binary = 0b0100001 // 2진수
var octal = 0o101 // 8진수
var hex = 0x41 // 16진수
```

- 자바스크립트의 숫자 타입은 정수만을 위한 타입이 없고 모든 수를 실수로 처리한다.

### 3가지의 특별한 값

```jsx
console.log(10 / 0); // Infinity
console.log(10 / -0); // -Infinity 
console.log(1 * 'String'); // NaN
```

### ⭐️문자열 타입

- 문자열은 0개 이상의 16비트 유니코드 문자들의 집합이다.
- 작은따옴표(' '), 큰따옴표(" "), 백틱(` `) 으로 감싸 사용한다.

```jsx
var string;
string = '문자열';
string = "문자열";
string = `문자열`;
```

### ⭐️템플릿 리터럴

- ES6부터 등장한 새로운 문자열 표기법
- 백틱(` `) 사용
- 멀티라인 문자열 / 표현식 삽입 / 태그드 템플릿

### 멀티라인 문자열

| 이스케이프 시퀀스 | 의미 | 출력 결과 | 예시 코드 | 출력 결과 |
| --- | --- | --- | --- | --- |
| `\0` | Null 문자 | 문자열 끝 | `console.log("A\0B")` | `AB` |
| `\'` | 작은따옴표 | `'` | `console.log('It\'s me')` | `It's me` |
| `\"` | 큰따옴표 | `"` | `console.log("He said \"Hi\"")` | `He said "Hi"` |
| `\\` | 백슬래시 | `\` | `console.log("C:\\Path")` | `C:\Path` |
| `\n` | 줄바꿈 | 개행 | `console.log("Hi\nThere")` | `Hi` `There` |
| `\r` | 캐리지 리턴 | 줄 앞으로 | `console.log("123\rA")` | `A23` |
| `\t` | 탭 | 수평 탭 | `console.log("A\tB")` | `A    B` |
| `\b` | 백스페이스 | 삭제 | `console.log("AB\bC")` | `AC` or `ABC` |
| `\f` | 폼 피드 | 페이지 나눔 | `console.log("A\fB")` | `AB` |
| `\v` | 수직 탭 | 수직 간격 | `console.log("A\vB")` | `AB` |

### 표현식 삽입

```jsx
var first = 'Ung-mo';
var last = 'Lee';
console.log(`My name is ${first} ${last}`); // 템플릿 리터럴
```

### ⭐️불리언 타입

```jsx
var foo = true;
console.log(foo);
foo = false;
console.log(foo);
```

### ⭐️undefined 타입

- 암묵적으로 undefined로 초기화됨
- 개발자가 의도적으로 사용 ❌ → 대신 null 사용 권장

### ⭐️null 타입

```jsx
var foo = 'lee';
foo = null; // 이전 참조 제거
```

### ⭐️심벌 타입

```jsx
var key = Symbol('key');
console.log(typeof key); // 'symbol'
var obj = {};
obj[key] = 'value';
console.log(obj[key]); // 'value'
```

### ⭐️객체 타입

- 거의 모든 것이 객체

### 데이터 타입이 필요한 이유

1. 메모리 공간의 크기 결정
2. 참조할 메모리 크기 결정
3. 2진수 해석 방식 결정

```jsx
var score = 100; // 숫자 타입 값 → 8바이트 메모리 확보
```

### ⭐️동적 타이핑

- 자바스크립트 변수는 **할당**에 의해 타입이 결정됨
- 재할당 시 타입도 변경 가능
- 자유롭지만 타입 안정성 부족