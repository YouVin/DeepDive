### ⭐️32.1 String 생성자 함수

<aside>
🔤

→ 표준 빌트인 객체 String 객체는 생성자 함수 객체다.

- new 연산자와 함께 호출하여 String 인스턴스를 생성할 수 있다.
- String 생성자 함수에 인수를 전달하지 않고 new 연산자와 호출하면
[[StringData]] 내부 슬롯에 빈 문자열을 할당한 String 래퍼 객체를 생성한다.

```jsx
const strObj = new String();
console.log(strObj); // String {length:0, [[PrimitiveValue]]:""}

// 1) new 없이 호출 → 원시 문자열 반환
console.log(String());   // ""

// 2) new와 함께 호출 → String 객체(래퍼 객체) 반환
console.log(new String());   // String {""}
```

→ String 생성자 함수의 인수로 문자열을 전달하면서 new 연산자와 호출하면?

- [[StringData]] 내부 슬롯에 인수로 전달받은 문자열을 할당한 String 래퍼 객체를 생성
- 배열과 유사하게 인덱스를 사용하여 각 문자에 접근할 수 있다.
- 단 문자열은 원시 값이므로 변경할 수 없다.
- 인수로 문자열 값이 아닌 값을 전달하면? → 강제변환 후 할당한다.
- new 연산자 없이 String 생성자 함수로 호출하면 문자열만 반환, + 타입 변환

```jsx
const strObj = new String('Lee');
console.log(strObj);
// String {0:'L', 1:'e', 2:'e', length: 3, [[PrimitiveValue]]:"Lee"}

// 배열과 유사하게 인덱스를 사용하여 문자에 접근하기
console.log(str[0]); // L

// 문자열은 원시 값이므로 변경할 수 없다. 에러는 발생 x
strObj[0] = 'S';
console.log(strObj); // 'Lee'

// 인수로 문자열 값이 아닌 값을 전달하면? → 강제변환 후 할당한다.
strObj = new String(null);
console.log(strObj); 
// String {0:'n', 1:'u', 2:'l' 3:'l', length: 4, [[PrimitiveValue]]:"null"}

// new 없이 호출 → 원시 문자열 반환 + 타입 변환
String(NaN); // -> "NaN"
String(true); // -> "true"
```

</aside>

### ⭐️32.2 length 프로퍼티

<aside>
🔤

→ length 프로퍼티는 문자열의 문자 개수를 반환한다.

- String 래퍼 객체는 배열과 마찬가지로 length 프로퍼티를 가지고 있다.
- String 래퍼 객체는 유사 배열 객체다.

```jsx
"hello".length; // -> 5
"안녕하세요!".length; // -> 6
```

</aside>

### ⭐️32.3 String 메서드

<aside>
🔤

→ 배열에는 두가지 방식의 메서드가 있다.

1. 원본을 직접 변경하는 메서드
2. 원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메서드

→ String 객체에는 원본 String 래퍼 객체를 직접 변경하는 메서드는 존재하지 않는다.

- String 객체의 메서드는 언제나 새로운 문자열을 반환한다.
- 문자열은 변경 불가능한 원시 값으로 String 래퍼 객체도 읽기 전용 객체이다.

```jsx
const strObj = new String('Lee');

console.log(Object.getOwnPropertyDescriptors(strObj));
// String 래퍼 객체는 읽기 전용 객체다.
{
	"0": {value: 'L', writable: false, enumerable: true, configurable: false },
	"1": {value: 'e', writable: false, enumerable: true, configurable: false },
	"2": {value: 'e', writable: false, enumerable: true, configurable: false },
	length: {value: 3, writable: false, enumerable: false, configurable: false },
}
// 읽기 전용이 아니게 된다면, 키 무결성이 무너지게 된다.	
```

</aside>

### **📌 32.3.1 String.prototype.indexOf**

<aside>
🔤

→ indexOf 메서드는 대상 문자열에서 인수로 전달받은 문자열을 검색하여 첫 번째 인덱스를 반환한다. 

- 검색에 실패할 시 -1을 반환한다.
- indexOf 메서드의 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.
- indexOf 메서드는 대상 문자열에 특정 문자열이 존재하는지 확인할 때 유용하다.
- ES6에서 도입된 String.prototype.includes 메서드를 사용하면 가독성이 좋다.

```jsx
const str = 'Hello World';

// 문자열 str에서 "l"을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf('l'); // -> 2

// 문자열 str에서 'or'를 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf('or'); // -> 7

// 문자열 str에서 'x'를 검색하여 첫 번째 인덱스를 반환한다. 검색에 실패 시 -1
str.indexOf('x'); // -> -1

// 문자열 str의 인덱스 3부터 'l'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf('l', 3); // -> 3

// Hello가 포함되어 있는지 확인.
if (str.indexOf('Hello') !== -1) {
	// 문자열 str에 'Hello'가 포함되어 있는 경우에 처리할 내용
}

if (str.includes('Hello')) {
	// 문자열 str에 'Hello'가 포함되어 있는 경우에 처리할 내용
}
```

</aside>

### **📌 32.3.2 String.prototype.search**

<aside>
🔤

→ search 메서드는 대상 문자열에서 인수로 전달받은 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환한다.

- 검색에 실패하면 -1을 반환한다.

```jsx
const str = 'Hello World';

// 문자열 str에서 정규 표현식과 매치하는 문자열을 검색하여 
// 일치하는 문자열의 인덱스를 반환한다.
str.search(/o/); // -> 4
str.search(/x/); // -> -1
```

</aside>

### **📌 32.3.3 String.prototype.includes**

<aside>
🔤

→ ES6에서 도입된 includes 메서드는 대상 문자열에 인수로 전달받은 문자열이 포함되어 있는지 확인하여 결과를 true 또는 false를 반환한다.

- 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

```jsx
const str = 'Hello World';

str.includes('Hello'); // -> true
str.includes(''); // -> true
str.includes('x'); // -> false
str.includes(); // -> false -> 이것은 includes(undefined) 와 같음

// 인덱스 3부터 포함되어 있는지 확인
str.includes('l', 3); // -> true
str.includes('H', 3); // -> false
```

</aside>

### **📌 32.3.4 String.prototype.startsWith**

<aside>
🔤

→ ES6에서 도입된 **startsWith**메서드는 대상 문자열이 인수로 전달받은 문자열로 시작하는지 확인하여 결과를 true 또는 false로 반환한다.

- **startsWith**메서드의 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

```jsx
const str = 'Hello World';

// 문자열 str이 'He'로 시작하는지 확인
str.startsWith('He'); // -> true
// 문자열 str이 'x'로 시작하는지 확인
str.startsWith('x'); // -> false
```

</aside>

### **📌 32.3.5 String.prototype.endsWith**

<aside>
🔤

→ ES6에서 도입된 endsWith 메서드는 대상 문자열이 인수로 전달받은 문자열로 끝나는지 확인하여 결과를 true 또는 false로 반환한다.

- endsWith 메서드의 2번째 인수로 검색할 문자열의 길이를 전달할 수 있다.

```jsx
const str = 'Hello world';

// 문자열 str이 'ld'로 끝나는지 확인
str.endsWith('ld'); // -> true
// 문자열 str이 'x'로 끝나는지 확인
str.endsWith('x'); // -> false

// 문자열 str의 처음부터 5자리까지('Hello')가 'lo'로 끝나는지 확인
str.endsWith('lo', 5); // -> true
```

</aside>

### **📌 32.3.6 String.prototype.charAt**

<aside>
🔤

→ charAt 메서드는 대상 문자열에서 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환한다.

- 문자열에서 **특정 위치(index)에 있는 문자**를 반환하는 메서드
- 인덱스는 문자열의 범위, 0 ~ 문자열 길이 -1 사이의 정수여야 한다.
- 인덱스가 문자열의 범위를 벗어난 정수인 경우 빈 문자열을 반환한다.

```jsx
const str = 'Hello';
for (let i = 0; i < str.length; i++) {
	console.log(str.charAt(i)); // H e l l o
}

// 인덱스가 문자열의 범위 (0 ~ str.length-1)를 벗어난 경우 빈 문자열을 반환
// str[5]는 undefined를 반환함
str.charAt(5); // -> ''
```

</aside>

### **📌 32.3.7 String.prototype.substring**

<aside>
🔤

→ substring 메서드는 대상 문자열에서 첫 번째 인수로 전달받은 인덱스에 위치하는 문자부터 두 번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 이전 문자까지의 부분 문자열을 반환한다.

- 두 번째 인수는 생략할 수 있다. → 첫 번째 인수부터 마지막 문자까지 부분 문자열을 반환
- **substring** 메서드의 첫 번째 인수는 두번째 인수보다 작아야 정상 아닌가? 
But. 가능하다.
- + 추가적으로 indexOf 메서드와 함께 사용하여 특정 문자열 기준으로 위치한 문자열을 취득할 수 있다.

```jsx
const str= 'Hello World';

// 인덱스 1부터 4이전까지의 부분 문자열을 반환한다.
str.substring(1, 4); // -> ell

// 인덱스 1부터 마지막 문자까지 부분 문자열을 반환한다.
str.**substring(1); // -> 'ello World';

//** 첫 번째 인수 > 두 번째 인수 인 경우 두 인수는 교환된다.
str.substring(4, 1); // -> 'ell'

// 인수 < 0 또는 NaN인 경우 0으로 취급 된다.
str.substring(-2); // -> 'Hello World'

// 인수 > 문자열의 길이(str.length)일 경우 인수는 문자열의 길이로 취급이다.
str.substring(1, 100); // -> 'ello World'
str.substring(20); // -> ''

// indexOf를 함께 사용하여 앞에 문자열 취득
str.substring(0, str.indexOf(' ')); // -> 'Hello' 0 ~ 5
// indexOf를 함께 사용하여 뒤에 문자열 취득
str.substring(str.indexOf(' ') + 1, str.length); // -> 'World' 6 ~ 끝
```

</aside>

### **📌 32.3.8 String.prototype.slice**

<aside>
🔤

→ slice 메서드는 substring 메서드와 동일하게 동작한다.
단, slice 메서드에는 음수인 인수를 전달할 수 있다.

- 음수인 인수를 전달하면 문자열의 가장 뒤에서부터 시작하여 문자열을 잘라내어 반환한다.

```jsx
const str = 'hello world';

// substring slice 메서드는 동일하게 동작한다.
// 0부터 5번째 이전 문자까지 잘라내어 반환.
str.substring(0, 5); // -> 'hello'
str.slice(O, 5); // -> 'hello'

// 인덱스가 2인 문자부터 마지막 문자까지 잘라내어 반환
str.substring(2); // -> 'llo world'
str.slice(2); // -> 'llo world'

// 인수 < 0 또는 NaN인 경우 0으로 취급된다.
str.substring(-5); // -> 'hello world'
// slice 메서드는 음수인 신루를 전달할 수 있다. 뒤에서 5자리를 잘라낸다.
str.slice(-5); // -> 'world'
```

</aside>

### **📌 32.3.9 String.prototype.toUpperCase**

<aside>
🔤

→ toUpperCase 메서드는 대상 문자열을 모두 대문자로 변경한 문자열을 반환한다.

```jsx
const str = 'Hello World!';
str.toUpperCase(); // -> 'HELLO WORLD!'
```

</aside>

### **📌 32.3.10 String.prototype.toLowerCase**

<aside>
🔤

→ toLowerCase 메서드는 대상 문자열을 모두 소문자로 변경한 문자열을 반환한다.

```jsx
const str = 'Hello World!';
str.toLowerCase (); // -> 'hello world!'
```

</aside>

### **📌 32.3.11 String.prototype.trim**

<aside>
🔤

→ trim 메서드는 대상 문자열 앞뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환한다.

- trimStart → 문자열 앞 공백 제거
- trimEnd → 문자열 뒤 공백 제거
- 정규 표현식을 인수로도 전달이 가능하다.

```jsx
const str = '        foo         ';
str.trim(); // -> foo

str.trimStart(); // -> 'foo          '
str.trimEnd(); // -> '         foo'
```

</aside>

### **📌 32.3.12 String.prototype.repeat**

<aside>
🔤

→ ES6에서 도입된 repeat 메서드는 대상 문자열을 인수로 전달받은 정수만큼 반복해 연결한 새로운 문자열을 반환한다.

- 인수로 전달받은 정수가 0이면 빈 문자열을 반환한다.
- 음수이면 RangeError가 발생한다.
- 인수를 생략하면 기본값 0이 설정된다.

```jsx
const str = 'abc';

str.repeat(); // -> ''
str.repeat(0); // -> ''
str.repeat(1); // -> 'abc'
str.repeat(2); // -> 'abcabc'
str.repeat(2.5); // -> 'abcabc' (2.5 -> 2)
str.repeat(-1); // RangeError
```

</aside>

### **📌 32.3.13 String.prototype.replace**

<aside>
🔤

→ replace 메서드는 대상 문자열에서 첫 번째 인수로 전달받은 문자열 또는 정규표현식을 검색하여 두 번째 인수로 전달한 문자열로 치환한 문자열을 반환한다.

```jsx
const str = 'Hello world';

// str에서 첫 번째 인수 'world'를 검색하여 두 번째 인수 'Lee'로 치환
str.replace('world', 'Lee'); // -> Hello Lee

// 검색된 문자열이 여럿 존재할 경우 첫 번째로 검색된 문자열만 치환한다.
const str = 'Hello world world';
str.replace('world', 'Lee'); // -> Hello Lee world

// 특수한 교체 패턴
const str = "Hello world";
console.log(str.replace('world', '<strong>$&</strong>'));
// "Hello <strong>world</strong>" $&은 현재 매칭된 문자열

// 메서드에 정규표현식을 인수로 전달 가능
// 'hello'를 대소문자를 구별하지 않고 전역 검색한다.
const str = "hello Hello hEllo guys";
const result = str.replace(/hello/gi, " Lee");

console.log(result);
// " Lee  Lee  Lee guys"
```

</aside>

### **📌 32.3.14 String.prototype.split**

<aside>
🔤

→ split 메서드는 대상 문자열에서 첫 번째 인수로 전달한 문자열 또는 정규 표현식을 검색하여 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환한다.

- 인수로 빈 문자열을 전달하면 각 문자를 모두 분리한다.
- 인수를 생략하면 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.
- 두 번째 인수로 배열의 길이를 지정할 수 있다.

```jsx
const str = 'How are you doing?';

// 공백으로 구분하여 배열로 반환한다.
str.split(' '); // -> ["How", "are", "you", "doing?"]

// \s는 여러가지 공백 문자를 의미한다.
str.split(/\s/); // -> ["How", "are", "you", "doing?"]

// 인수로 빈 문자열을 전달하면 각 문자를 모두 분리한다.
str.split('');
// -> ["H", "o", "w, " ", "a", "r", "e", " ", "y", "o", "u", " ", "d", "o", "i"
// "n", "g", "?"]

// 인수를 생략하면 대상 문자열 전체를 단일 요소로 하는 배열을 반환
str.split(); // -> ["How are you doing?"]

// 두 번째 인수로 배열의 길이를 지정할 수 있다.
str.split(' ', 3); // -> ["how", "are", "you"]

// split 메서드는 배열을 반환한다. 
// reverse + join으로 역순으로 반환이 가능하다.
function reverseString(str) {
	return str.split('').reverse().join('');
}
reverseString('Hello world!'); //-> '!dlrow olleH'

```

</aside>