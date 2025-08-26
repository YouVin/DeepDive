### ⭐️27.1 배열이란?

<aside>
📖

→ 배열은 여러 개의 값을 순차적으로 나열한 자료구조이다.

`const arr = [’apple’, ‘banana’, ‘orange’];`

- 배열이 가지고 있는 값을 요소라고 부른다. → 자바스크립트의 모든 값은 요소가 될 수 있다.
- 배열의 요소는 배열에서 자신의 위치를 나타내는 0 이상의 정수인 인덱스를 갖는다.
- 요소에 접근할 때는 대괄호 표기법을 사용한다.

```jsx
arr[0] // -> 'apple'
arr[1] // -> 'banana'
arr[2] // -> 'orange'

// 배열은 요소의 개수, 배열의 길이를 나타내는 length 프로퍼티를 갖는다
arr.length // -> 3

// 배열은 인덱스와 length 프러파티를 갖기에 for문을 통해 요소에 접근이 가능하다.
for( let i = 0; i < arr.length; i++ ) {
	console.log(arr[i]); // 'apple' 'banana' 'orange'
}

// 자바스크립트에 배열이라는 타입은 존재하지 않는다, 배열은 객체 타입이다.
typeof arr // -> object

// 배열은 리터럴, Array 생성자 함수, Array.of, Array.from 메서드로 생성할 수 있다.
const arr = [1, 2, 3]
arr.constructor === Array // -> true
Object.getPrototypeOf(arr) === Array.prototype // -> true
```

→ 배열은 객체지만 일반 객체와는 구별되는 독특한 특징이 있다.

| 구분 | 객체 | 배열 |
| --- | --- | --- |
| 구조 | 프러퍼티 키와 프로퍼티 값 | 인덱스와 요소 |
| 값의 참조 | 프로퍼티 키  | 인덱스 |
| 값의 순서 | x  | o |
| length 프로퍼티 | x | o |

→ 배열의 장점

- 처음부터 순차적으로 요소에 접근할 수 있다.
- 마지막부터 역순으로 요소에 접근할 수 있다.
- 특정 위치부터 순차적으로 요소에 접근할 수 있다.
</aside>

### ⭐️27.2 자바스크립트 배열은 배열이 아니다.

<aside>
💦

→ 자료구조에서 말하는 배열?

- 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조를 말한다.
- 배열의 요소 하나의 데이터 타입으로 통일되어 있으며 서로 연속적으로 인접해 있다.
- 이런한 배열을 밀집 배열이라 한다.

→ 주요 특징

1. 연속적 메모리
- 모든 원소가 **빈틈없이 이어진 메모리 공간**에 배치됨.
- CPU가 인덱스를 이용해 해당 원소의 위치를 수학적으로 바로 계산할 수 있음.
1. 단일 데이터 타입
- 배열의 모든 요소는 같은 크기의 자료형으로 통일.
- 이 덕분에 인덱스 기반 접근이 가능해짐.

→ 희소 배열(Sparse Array)

희소 배열은 **인덱스 범위에 비해 실제로 저장된 데이터의 개수가 적은 배열**

즉, 요소들 사이에 “비어 있는 칸(값이 없음 or 기본값)”이 많이 있는 배열 구조

→ 자바스크립트 배열은 일반적인 배열의 동작을 흉내 낸 특수한 객체다.

```jsx
console.log(Object.getOwnPropertyDescriptors([1, 2, 3]);
{
	'0': {value: 1, writable: true, enumerable: true, configurable: true}
	'1': {value: 2, writable: true, enumerable: true, configurable: true}
	'2': {value: 3, writable: true, enumerable: true, configurable: true}
	length: {value: 3, writable: true, enumerable: false, configurable: false}
}
```

→ 배열 안 요소에는 사용할 수 있는 모든 값은 객체의 프로퍼티가 될 수 있으므로 어떤 타입의 값이라도 배열의 요소가 될 수 있다.

```jsx
const arr = [
	'string',
	10,
	true,
	null,
	undefined,
	NaN,
	Infinity,
	[ ],
	{ },
	function () {}
];
```

→ 인덱스로 배열 요소로 접근할 때 단점

- 해시 테이블로 구현된 객체로 인덱스로 요소에 접근하는 경우 일반적인 배열보다 느리다.
- 모던 자바스크립트 엔진은 배열을 일반 객체와 구별하여 좀 더 배열처럼 동작하도록 최적화하여 구현했다.

```jsx
const arr = [];

console.time('Array Performance Test');

for (let i = 0; i < 10000000; i++) {
	arr[i] = i;
}
console.timeEnd('Array Performance Test');
// 약 340ms

const obj = {};
console.time('Object Performance Test');

for(let i = 0; i < 10000000; i++) {
	obj[i] = i;
}

console.timeEnd('Object Performance Test');
// 약 600ms
```

</aside>

### ⭐️27.3 length 프로퍼티와 희소 배열

<aside>
🤼‍♀️

→ length 프로퍼티는 요소의 개수, 배열의 길이를 나타내는 0 이상의 정수를 값으로 갖는다.

- length 프로퍼티의 값은 빈 배열일 경우 0이며, 빈 배열이 아닐 경우 가장 큰 인덱스에 1을 더한 것과 같다.

```jsx
[].length // -> 0
[1, 2, 3].length // -> 3
```

- length 프로퍼티의 값은 2의 32승 - 1 미만의 양의 정수다. 즉 배열의 요소를 최대 (4,294,967.295)개 가질 수 있다. 배열에서 사용할 수 있는 가장 작은 인덱스는 0이다.

→ length 프로퍼티의 값은 배열에 요소를 추가하거나 삭제하면 자동 갱신된다.

```jsx
const arr = [1, 2, 3];
console.log(arr.length); // 3

// 요소 추가
arr.push(4);
// 요소를 추가하면 프로퍼티 값이 자동으로 갱신된다.
console.log(arr.length); // 4

// 요소 삭제
arr.pop();
// 요소를 삭제하면 프로퍼티 값이 자동으로 갱신된다.
console.log(arr.length); // 3

// 현재 length 프로퍼티 값보다 작은 숫자 값을 할당하면 배열의 길이가 줄어든다.
arr = [1, 2, 3, 4, 5];

// 현재 length 프러퍼티 값인 5보다 작은 3으로 할당
arr.length = 3;
console.log(arr); // [1, 2, 3]

// 현재 length 보다 큰 숫자로 할당은 x
arr.length = 5;
console.log(arr); // [1, 2, 3, empty, empty] 값 존재 x
// 프로퍼티 값은 성공적으로 변하지만, 배열에는 아무런 변함 없다.
// 값 없이 비어있는 요소를 위해 메모리 공간을 확보하지 않으며 빈 요소를 생성 x
```

→ 회소 배열이란?

- 배열의 요소가 연속적으로 위치하지 않고 일부가 비어 있는 배열을 희소 배열이라 한다.

```jsx
// 희소 배열
const sparse = [ , 2, , 4];

// 희소 배열의 length 프로퍼티 값은 요소의 개수와 일치하지 않는다.
console.log(sparse.length); // 4
console.log(sparse); // [empty, 2, empty, 4]

// 배열 sparse에는 인덱스가 0, 2인 요소가 존재하지 않는다.
```

- 희소 배열은 length와 배열 요소의 개수가 일치하지 않는다.
- 희소 배열의 length는 희소 배열의 실제 요소 개수보다 언제나 크다.
- 배열을 생성할 경우에는 희소 배열을 생성하지 않도록 주의하자, 배열에는 같은 타입의 요소를 연속적으로 위치시키는것이 최선이다.
</aside>

### ⭐️27.4 배열 생성

### **📌 27.4.1 배열 리터럴**

<aside>
🤼‍♀️

→ 배열에도 다양한 생성 방식이 있다.

- 가장 일반적이고 간편한 배열 생성 방식은 배열 리터럴이다.
- 배열 리터럴은 0개 이상의 요소를 쉼표로 구분하여 대괄호로 묶는다.
- 배열 리터럴은 객체 리터럴과 달리 프로퍼티 키가 없고 값만 존재한다.

```jsx
const arr = [1, 2, 3];
console.log(arr.length); // 3

// 배열 리터럴에 요소를 하나도 추가하지 않는다면?
const arr = [];
console.log(arr.length); // 0

// 배열 리터럴에 요소를 생략하면 ?
const arr = [1, , 3]; // 희소 배열
// 희소 배열의 length는 배열의 실제 요소 개수보다 언제나 크다.
console.log(arr.length); // 3
console.log(arr); // [1, empty, 3]
console.log(arr[1]); // undefined
```

</aside>

### **📌 27.4.2 Array 생성자 함수**

<aside>
💂

→ Object 생성자 함수를 통해 객체를 생성 하듯이 Array 생성자 함수를 통해 배열을 생성할 수도 있다.

- Array 생성자 함수는 전달된 인수의 개수에 따라 다르게 동작하므로 주의가 필요하다.

```jsx
// 전달된 인수가 1개 이고 숫자인 경우 length가 인수인 배열을 생성한다.
const arr = new Array(10);

console.log(arr); // [empty * 10]
console.log(arr.length); // 10
// 희소 배열. length 프로퍼티 값은 0이 아니지만 배열의 요소에는 존재하지 않는다.

// 전달된 인수가 없는 경우 빈 배열을 생성한다. 즉 배열 리터럴 []과 같다.
new Array(); // -> []

// 전달된 인수가 2개 이상이거나 숫자가 아닌 경우 인수를 요소로 갖는 배열을 생성
new Array(1, 2, 3); // -> [1, 2, 3]
// 전달된 인수가 1개지만 숫자가 아니면 인수를 요소로 갖는 배열을 생성
new Array({}); // -> [{}]

// Array 생성자 함수는 new 연산자와 함께 호출하지 않고 일반함수
// 로서 호출해도 배열을 생성하는 생성자 함수로 동작한다.
Array(1, 2, 3); // -> [1, 2, 3]
```

</aside>

### **📌 27.4.3 Array.of**

<aside>
🧑‍🔧

→ ES6에서 도입된 Array.of 메서드는 전달된 인수를 요소로 갖는 배열을 생성한다.

```jsx
// 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성한다.
Array.of(1); // -> [1]
Array.of(1, 2, 3); // -> [1, 2, 3]
Array.of('string'); // -> ['string']
```

</aside>

### **📌 27.4.4 Array.from**

<aside>
🧑‍🔧

→ ES6에서 도입된 Array.from 메서드는 유사 배열 객체 또는 이터러블 객체를 인수로 전달받아 배열로 변환하여 반환한다.

```jsx
// 유사 배열 객체를 변환하여 배열 생성
Array.from({ length: 2, 0: 'a', 1: 'b' }); // -> ['a', 'b']
// 이터러블을 변환하여 배열을 생성한다. 문자열은 이터러블이다.
Array.from('Hello'); // -> ['H', 'e', 'l', 'l', 'o']

// Array.from에 length만 존재하는 유사 배열 객체를 전달하면, undefined
Array.from({ length: 3}); // -> [undefined, undefined, undefined]
// Array.from은 두 번째 인수로 전달한 콜백 함수의 반환값으로 구성된 배열을 반환
Array.from({ length: 3}, (_,i) => i); // -> [0, 1, 2]
```

</aside>

### ⭐️27.5 배열 요소의 참조

<aside>
🧗

→ 배열의 요소를 참조할 때에는 대괄호([]) 표기법을 사용한다.

- 대괄호 안에는 인덱스가 와야한다.
- 정수로 평가되는 표현식이라면 인덱스 대신 사용할 수 있다.

```jsx
const arr = [1, 2];

// 인덱스가 0인 요소를 참조
console.log(arr[0]); // 1
// 인덱스가 1인 요소를 참조
console.log(arr[1]); // 2

// 존재하지 않는 요소에 접근하면 undefined가 반환된다.
console.log(arr[2]); // undefined

// 희소배열의 존재하지 않는 요소를 참조해도 undefined가 반환된다.
// 희소배열
const arr = [1, ,3];
// 배열 arr에는 인덱스가 1인 요소가 존재하지 않는다.
console.log(arr[1]); // undefined 
```

</aside>

### ⭐️27.6 배열 요소의 추가와 갱신

<aside>
🧗

→ 객체에 프로퍼티를 동적으로 추가할 수 있는 것처럼 배열에도 요소를 동적으로 추가할 수 있다.

- 존재하지 안는 인덱스를 사용해 값을 할당하면 새로운 요소가 추가된다, length도 자동갱신

```jsx
const arr = [0];

// 배열 요소의 추가
arr[1] = 1;
console.log(arr); // [0, 1]
console.log(arr.length); // 2
```

→ 현재 배열의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 희소 배열이 된다.

```jsx
arr[100] = 100;
console.log(arr); // [0 , 1, empty * 98, 100]
console.log(arr.length); // 101

// 명시적으로 값을 할당하지 않은 요소는 생성되지 않는다.
console.log(Object.getOwnPropertyDescriptor(arr));
// 0, 1, 100 length 만 뜬다.

// 요소값 재할당 시 요소값이 갱신
arr[1] = 10;
console.log(arr); // [0, 10, empty * 98, 100]
```

→ 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아닌 프로퍼티가 생성된다.

- 추가된 프로퍼티는 length 값에 영향을 주지 않는다.

```jsx
const arr = [];

// 배열 요소의 추가
arr[0] = 1;
arr['1'] = 2;

// 프로퍼티 추가
arr['foo'] = 3;
arr.bar = 4;
arr[1.1] = 5;
arr[-1] = 6;

console.log(arr); // [1, 2, foo: 3, bar:4, '1.1': 5, '-1': 6]
// 프로퍼티는 length에 영향을 주지 않는다.
console.log(arr.length); // 2
```

</aside>

### ⭐️27.7 배열 요소의 삭제

<aside>
🧜

→ 배열은 사실 객체이기 때문에 배열의 특정 요소를 삭제하기 위해 delete 연산자를 사용할 수 있다.

```jsx
const arr = [1, 2, 3];

// 배열 요소의 삭제
delete arr[1]; 
console.log(arr); // [1, empty, 3]

// length 프로퍼티에 영향을 주지 않는다. 희소배열
console.log(arr.length); // 3
```

→delete 연산자는 객체의 프로퍼티를 삭제한다. 

- 위 예제에서 삭제 시 배열은 희소 배열이 되며  length 프로퍼티 값은 변하지 않는다. 따라소 희소 배열을 만드는 delete는 사용하지 않는게 좋다.

```jsx
const arr = [1, 2, 3];

// Array.prototype.splice(삭제를 시작할 인덱스, 삭제할 요소 수)
// arr[1] 부터 1개 요소 제거
arr.splice(1, 1);
console.log(arr); // [1, 3]

// length 프로퍼티가 자동 갱신된다.
console.log(arr.length); // 2
```

</aside>

### ⭐️27.8 배열 메서드

<aside>
👳‍♂️

→ 자바스크립트는 배열을 다룰 때 유용한 다양한 빌트인 메서드를 제공한다.

- Array 생성자 함수는 정적 메서드를 제공
- 배열 객체의 프로토 타입인 Array.prototype은 프로토타입 메서드를 제공

→ 배열 메서드 결과물을 반환하는 패턴 2가지

1. 배열에는 원본 배열을 직접 변겨아는 메서드
2. 원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메서드

```jsx
const arr = [1];

// push 메서드는 원본 배열(arr)을 직접 변경한다.
arr.push(2);
console.log(arr); // [1, 2]

// concat 메서드는 원본 배열을 직접 변경하지 않고 새로운 배열을 반환한다.
const result = arr.concat(3);
console.log(arr); // [1, 2]
console.log(result); // [1, 2, 3]
```

</aside>

### **📌 27.8.1 Array.isArray**

<aside>
🍁

→ Array.isArray는 Array 생성자 함수의 정적 메서드다.

- Array.isArray 메서드는 전달된 인수가 배열이면 true, 배열이 아니면 false 반환한다.

```jsx
// true 
Array.isArray([]);
Array.isArray([1, 2]);
Array.isArray(new Array());

// false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(1);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
Array.isArray({ 0: 1, length: 1 })
```

</aside>

### **📌 27.8.2 Array.prototype.indexOf**

<aside>
🍁

→ indexOf 메서드는 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.

- 원본 배열에 인수로 전달한 요소와 중복되는 요소가 여러 개 있다면 첫 번째로 검색된 요소의 인덱스를 반환한다.
- 원본 배열에 인수로 전달한 요소가 존재하지 않으면 -1을 반환한다.

```jsx
const arr = [1, 2, 2, 3];
// 배열 arr에서 요소 2를 검색하여 첫 번째로 검색된 요소의 인덱스를 반환한다.
arr.indexOf(2); // 1
// 배열 arr에 요소 4가 없으므로 -1을 반환한다.
arr.indexOf(4); // -1
// 두 번째 인수는 검색을 시작할 인덱스다, 두 번째 인수를 생랴가면 처음부터 검색
arr.indexOf(2, 2); // 2

// indexOf는 배열에 특정 요소가 존재하는지 확인할 때 유용하다.
const foods = ['apple', 'banana', 'orange'];
// foods 배열에 'orange' 요소가 존재하는지 확인한다.
if(foods.indexOf('orange') === -1) {
	foods.push('orange');
}
console.log(foods); // ['apple', 'banana', 'orange']

// indexOf 메서드 대신 ES7에서 도입된 Array.prototype.includes 메서드를 사용하자.
if(!foods.includes('orange')){
	foods.push('orange');
}
console.log(foods); // ['apple', 'banana', 'orange']
```

</aside>

### **📌 27.8.3 Array.prototype.push**

<aside>
🍁

→ push 메서드는 인수로 전달받은 모든 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.

- push 메서드는 원본 배열을 직접 변경한다.

```jsx
const arr = [1, 2];

// 인수로 전달받은 모든 값을 원본 배열 arr의 마지막 요소로 추가
// 변경된 length 값을 반환한다.
let result = arr.push(3, 4);
console.log(result); // 4
// push 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 2, 3, 4]
```

→ push 메서드는 성능 면에서 좋지 않다.

- 마지막 요소로 추가할 요소가 하나뿐이라면 push 메서드를 사용하지 않고 length 프로퍼티를 사용하여 배열 마지막에 요소를 직접 추가 가능하다.

```jsx
const arr = [1, 2];
// arr.push(3)과 동일한 처리이다. push 메서드보다 빠름.
arr[arr.length] = 3;
console.log(arr); // [1, 2, 3]
```

→ push 메서드는 원본 배열을 변경하는 부수 효과가 있다.

```jsx
const arr = [1, 2];

// ES6 스프레드 문법
const newArr[...arr, 3];
console.log(newArr); // [1, 2, 3]
```

</aside>

### **📌 27.8.4 Array.prototype.pop**

<aside>
🍁

→ pop 메서드는 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.

- 원본 배열이 빈 배열이면 undefined를 반환한다.
- pop 메서드는 원본 배열을 직접 변경한다.

```jsx
const arr = [1, 2];
// 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.
let result = arr.pop();
console.log(result); // 2
// pop 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1]
```

</aside>

### **📌 27.8.5 Array.prototype.unshift**

<aside>
🍁

→ unshift 메서드는 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.

- unshift 메서드는 원본 배열을 직접 변경한다.

```jsx
const arr = [1, 2];
// 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 
// length 값을 반환한다.
let result = arr.unshift(3, 4);
console.log(result); // 4
// unshift 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [3, 4, 1, 2]
```

→ unshift 메서드는 원본 배열을 직접 변경하는 부수 효과가 있다.

```jsx
// 따라서 스프레드 문법을 이용하자
const arr = [1, 2];
// ES6 스프레드 문법
const newArr = [3, ...arr];
console.log(newArr); // [3, 1, 2]
```

</aside>

### **📌 27.8.6 Array.prototype.shift**

<aside>
🍁

→ shift  메서드는 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.

- 원본 배열이 빈 배열이면 undefined를 반환한다.

```jsx
const arr = [1, 2];

// 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.
let result = arr.shift();
console.log(result); // 1

// shift 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [2]
```

</aside>

### **📌 27.8.7 Array.prototype.concat**

<aside>
🍁

→ concat 메서드는 인수로 전달된 값들을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다.

- 인수로 전달한 값이 배열인 경우 배열을 해체하여 새로운 배열의 요소로 추가한다.
- 원본 배열은 변경되지 않는다.

```jsx
const arr1 = [1, 2];
const arr2 = [3, 4];

// 배열 arr2를 원본 배열 arr1의 마지막 요소로 추가한 새로 배열을 반환한다.
// 인수로 전달한 값이 배열인 경우 배열을 해체하여 새로운 배열의 요소로 추가한다.
let result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4]

// 숫자를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환한다.
result = arr1.concat(3);
console.log(result); // [1, 2, 3,]

// 배열 arr2와 숫자를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환한다.
result = arr1.concat(arr2, 5);
console.log(result); // [1, 2, 3, 4, 5];

// 원본 배열은 변경되지 않는다.
console.log(arr1); // [1, 2]
```

→ concat 메서드는 ES6 스프레드 문법으로 대체할 수 있다.

```jsx
let result = [1, 2].concat([3, 4]);
console.log(result); // [1, 2, 3, 4]

// concat 메서드는 ES6 스프레드 문법으로 대체할 수 있다.
result = [...[1, 2], ...[3, 4]];
console.log(result); // [1, 2, 3, 4]
```

</aside>

### **📌 27.8.8 Array.prototype.splice**

<aside>
🍁

→ 원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우 splice 메서드를 사용한다.

- start: 원본 배열의 요소를 제거하기 시작할 인덱스다. start 만 지정하면 원본 배열의 start부터 모든 요소를 제거한다.
start가 음수인 경우 배열의 끝에서의 인덱스를 나타낸다.
만약 start -1 이며 마지막 요소를 가지키고 -n 마지막에서 n 번재 요소를 가리킨다.
- deleteCount: 원본 배열의 요소를 제거하기 시작할 인덱스인 start부터 제거할 요소의 개수다.
deleteCount가 0인 경우 아무런 요소도 제거되지 않는다.
- items: 제거한 위치에 삽입할 요소들의 목록이다. 생략할 경우 원본 배열에서 요소들을 제거하기만 한다.

```jsx
const arr = [1, 2, 3, 4];

// 원본 배열의 인덱스 1부터 2개의 요소를 제거하고 그 자리에 새로운 요소 
// 20, 30 을 삽입한다.
const result = arr.splice(1, 2, 20, 30);

// 제거한 요소가 배열로 반환된다.
console.log(result); // [2, 3]
// splice 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 20, 30, 4]
```

→ splice 메서드의 두 번째 인수를 0으로 지정하면 아무런 요소도 제거하지 않고 새로운 요소들을 삽입한다.

```jsx
const arr = [1, 2, 3, 4];

// 원본 배열의 인덱스 1부터 0개의 요소를 제거하고 그 자리에 새로운 요소 100 삽입
const result = arr.splice(1, 0, 100);

// 원본 배열이 변경된다.
console.log(arr); // [1, 100, 2, 3, 4]
// 제거한 요소가 배열로 반환된다.
console.log(result); // []

// + 제거한 위치에 추가할 요소를 전달하지 않으면 원본 배열에서 제거만 한다.
arr = [1, 2, 3, 4];
// 원본 배열의 인덱스 1부터 2개의 요소를 제거한다.
const result = arr.splice(1, 2);

// 원본 배열이 변경된다.
console.log(arr); // [1, 4]
// 제거할 요소가 배열로 반환된다.
console.log(result); // [2, 3]

// ++ 제거할 요소의 개수를 생략하면 시작 인덱스부터 모든 요소를 제거한다.
arr = [1, 2, 3, 4];
// 원본 배열 인덱스 1부터 모든 요소를 제거한다.
const result = arr.splice(1);

// 원본 배열이 변경된다.
console.log(arr); // [1]
// 제거한 요소가 배열로 반환된다.
console.log(result); // [2, 3, 4]
```

→ filter 메서드를 사용하여 특정요소 제거하기

- 특정 요소가 중복된 경우 모두 제거된다.

```jsx
const arr = [1, 2, 3, 1, 2];

// 배열 array에서 모든 item 요소를 제거한다.
function removeAll(array, item) {
	return array.filter(v => v !== item);
}

console.log(removeAll(arr, 2)); // [1 ,3, 1]
```

</aside>

### **📌 27.8.9 Array.prototype.slice**

<aside>
🍁

→ slice 메서드는 인수로 전달된 범위의 요소들을 복사하여 배열로 반환한다.

- 원본 배열은 변경되지 않는다.
- 이름이 유사한 splice 메서드는 원본 배열을 변경하므로 주의하기

→ slice 메서드는 두개의 매개변수를 갖는다.

- start : 복사를 시작할 인덱스, 음수인 경우 배열 끝에서의 인덱스를 나타낸다.
- end: 복사를 종료할 인덱스, 이 인덱스에 해당하는 요소는 복사되지 않는다.

```jsx
const arr = [1, 2, 3];

// arr[0] 부터 arr[1] 까지 복사하여 반환하기
arr.slice(0, 1); // -> [1]
// arr[1] 부터 arr[2] 까지 복사하여 반환하기
arr.slice(1, 2); // -> [2]
// 원본은 변경되지 않는다.
console.log(arr); // [1, 2, 3]

// + 두번째 인수 생략 시 첫 번째 인수 이후 모든 요소 복사하기
arr.slice(1); // -> [2, 3]

// + 첫 번째 인수가 음수이면 끝에서부터 복사
arr.slice(-1); // -> [3]
arr.slice(-2); // -> [2, 3]

// + 모든 인수를 생략하면 원본 배열의 복사본 생성
const copy = arr.slice();
console.log(copy); // [1, 2, 3] -> 이때 생성된 배열은 얕은 복사이다.

// + ES6 이터러블 객체로 배열 간단하게 변환하기
function sum() {
	// 이터러블을 배열로 변환
	const arr = [...arguments];
	console.log(arr); // [1, 2, 3]
	return arr.reduce((pre, cur) => pre + cur, 0);
}
console.log(sum(1, 2, 3)); // 6
```

</aside>

### **📌 27.8.10 Array.prototype.join**

<aside>
🍁

→ join 메서드는 원본 배열의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 문자열, 즉 구분자로 연결한 문자열을 반환한다.

```jsx
const arr = [1, 2, 3, 4];

// 기본 구분자는 콤마다.
// 원본 배열 arr의 모든 요소를 문자열로 변환한 후 기본 구분자로 연결한 문자열 반환
arr.join(); // -> '1, 2, 3, 4'
// 원본 배열 arr 의 모든 요소를 문자열로 변환한 후 빈 문자열로 연결한 문자열 반환
arr.join(''); // -> '1234'
// 원본 배열 arr의 모든 요소를 문자열로 변환 후 구분자':'로 연결한 문자열 반환
arr.join(':'); // -> '1:2:3:4'
```

</aside>

### **📌 27.8.11 Array.prototype.reverse**

<aside>
🍁

→ reverse 메서드는 원본 배열의 순서를 반대로 뒤집는다. 

- 원본 배열이 변경된다.
- 반환 값은 변경된 배열이다.

```jsx
const arr = [1, 2, 3];
const result = arr.reverse();

// reverse 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [3, 2, 1]
// 반환값은 변경된 배열이다.
console.log(result); // [3, 2, 1]
```

</aside>

### **📌 27.8.12 Array.prototype.fill**

<aside>
🍁

→ ES6에서 도입된 fill 메서드는 인수로 전달받은 값을 배열의 처음부터 끝까지  요소로 채운다.

- 원본 배열이 변경된다.

```jsx
const arr = [1, 2, 3];
// 인수로 전달받은 값 0을 처음 . 끝 까지 요소로 채운다.
arr.fill(0);
// fill 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [0, 0, 0]

// + 두 번째 인수로 ㅇ소 채우기를 시작할 인덱스를 전달할 수 있다.
// 인수로 전달받은 값 0을 배열의 인덱스 1부터 끝까지 요소로 채운다.
arr.fill(0, 1);
// fill 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 0, 0]

// + 세 번째 요소 채우기를 멈출 인덱스를 전달할 수 있다.
arr = [1, 2, 3, 4, 5];
// 인수로 전달받은 값 0을 배열의 인덱스 1부터 3 이전까지 요소로 채운다.
arr.fill(0, 1, 3);
// fill 메서드 원본 배열을 직접 변경한다.
console.log(arr); // [1, 0, 0, 4, 5]

// + fill 메서드를 사용하면 배열을 생성하면서 특정 값으로 요소를 채울 수 있다.
arr = new Array(3);
console.log(arr); // [empty * 3]
// 인수로 전달받은 값 1을 배열 처음부터 끝까지 요소로 채운다.
const result = arr.fill(1);
// 원본 배열 직접 변경
console.log(arr); // [1, 1, 1] 
```

</aside>

### **📌 27.8.13 Array.prototype.includes**

<aside>
🍁

→ ES7에서 도입된 includes 메서드는 배열 내에 특정 요소가 포함되어 있는지 확인하여

true 또는 false를 반환한다.

- NaN 확인이 가능하다.

```jsx
const arr = [1, 2, 3];
// 배열에 요소 2가 포함되어 있는지 확인한다.
arr.includes(2); // -> true
// 배열에 ㅇ소 100이 포함되어 있는지 확인한다.
arr.includes(100); // -> false

// + 두번재 인수로 검색을 시작할 인덱스 전달할 수 있다.
// 배열 요소 1이 포함되어 있는지 인덱스 1부터 확인
arr.includes(1, 1); // -> false
// 배열에 ㅇ소 3이 포함되어 있는지 인덱스 2부터 확인
arr.includes(3, -1); // -> true
```

</aside>

### **📌 27.8.14 Array.prototype.flat**

<aside>
🍁

→ ES10에서 도입된 flat 메서드는 인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화 한다.

```jsx
[1, [2, 3, 4, 5]].flat(); // -> [1, 2, 3, 4, 5]

// 중첩 배열을 평탄화하기 위한 깊이 값의 기본 값은 1이다.
[1, [2, [3, [4]]].flat(); // -> [1, 2, [3, [4]]]
[1, [2, [3, [4]]].flat(1); // -> [1, 2, [3, [4]]]

// 중첩 배열을 평탄화하기 위한 깊이 값을 2로 지정하여 2단계 깊이까지 평탄화
[1, [2, [3, [4]]].flat(2); // -> [1, 2, 3, [4]]
// 2번 평탄화 한 것과 동일하다
[1, [2, [3, [4]]].flat().flat(); // -> [1, 2, 3, [4]]
// 중첩 배열을 평탄화하기 위한 깊이 값을 Infinity로 지정하여 모두 평탄화
[1, [2, [3, [4]]].flat(Infinity); // -> [1, 2, 3, 4]
```

</aside>

### ⭐️27.9 배열 고차 함수

<aside>
🍁

→ 고차 함수는 함수를 인수로 전달받거나 함수를 반환하는 함수를 말한다.

- 고차 함수는 외부 상태의 변경이나 가변 데이터를 피하고 불변성을 지향한다.
- 순수 함수를 통해 부수효과를 최대한 억제하여 오류를 피하고 안정성을 높인다.
</aside>

### **📌 27.9.1 Array.prototype.sort**

<aside>
🍁

→ sort 메서드는 배열의 요소를 정렬한다. 

- 원본 배열을 직접 변경하고 정렬된 배열을 반환한다.
- sort 메서드는 기본적으로 오름차순으로 요소를 정렬한다.

```jsx
const fruits = ['Banana', 'Orange', 'Apple'];
// 오름차 순 정렬
fruits.sort();
// sort 메서드는 원본 배열을 직접 변경한다.
console.log(fruits); // ['Apple', 'Banana', 'Orange']

// 한글도 가능하다.
// 내림차 순은 reverse를 사용한다.
fruits.reverse();
console.log(fruits); // ['Orange', 'Banana', 'Apple']
```

→ 숫자 요소를 정렬할때는 주의가 필요하다.

- 유니코드 코드 포인의 순서를 따른다.
- 숫자 타입이라 할지라도 배열의 요소를 일시적으로 문자열로 변환 후 유니코드 코드 포인의 순서로 정렬한다.
- 따라서 숫자요소를 정렬할 때는 sort 메서드에 정렬 순서를 정의하는 비교함수를 인수로 전달한다.

```jsx
const points = [40, 100, 1, 5, 2, 25, 10];

// 숫자 배열의 오름차순 정렬
points.sort((a, b) => a - b);
console.log(points); // [1, 2, 5, 10, 25, 45, 100]

// 숫자 배열의 내림차순 정렬
points.sort((a, b) => b - a);
console.log(points); // [100, 45, 25, 10, 5, 2, 1]
```

</aside>

### **📌 27.9.2 Array.prototype.forEach**

<aside>
🍁

→ for문을 대체할 수 있는 고차 함수다.

- forEach 메서드는 자신의 내부에서 반복문을 실행한다.
- 반복문을 통해 자신을 호출한 배열을 순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출한다.

```jsx
const numbers = [1, 2, 3];
const pows = [];
// forEach 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출
numbers.forEach(item => pows.push(item ** 2));
console.log(pows); // [1, 4, 9]

// forEach 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달
[1, 2, 3].forEach((item, index, arr) => {
	console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
});
// 요소값 : 1 인덱스 : 0 this: [1,2,3]
// 요소값 : 2 인덱스 : 1 this: [1,2,3]
// 요소값 : 3 인덱스 : 2 this: [1,2,3]
```

→ forEach 메서드는 원본 배열을 변경하지 않는다.

- 콜백함수를 통해 원본 배열을 변경할 수 있다.

```jsx
const numbers = [1, 2, 3];
numbers.forEach((item, index, arr) => { arr[index] = item ** 2; });
console.log(numbers); // [1, 4, 9]

// forEach 메서드의 반환값은 언제나 undefined다.
const result = [1, 2, 3].forEach(console.log);
console.log(result); // undefined
```

</aside>

### **📌 27.9.3 Array.prototype.map**

<aside>
🍁

→ map 메서드는 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다.

- 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.
- 원본 배열은 변경되지 않는다.

```jsx
const numbers = [ 1, 4, 9 ];
// map 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수르 반복 호출
// 콜백 함수의 반환값들로 구성된 새로운 배열 반환
const roots = numbers.map(item => Math.sqrt(item)); 
console.log(roots); // [1, 2, 3]
console.log(numbers); // [1 ,4, 9]
```

→ map 메서드가 생성하여 반환하는 새로운 배열의 length 프로퍼티 값은 map ㅔㅁ서드를 호출한 배열의 length 프로퍼티 값과 반드시 일치한다.

- map 메서드를 호출한 배열과 map 메서드가 생성하여 반환한 배열은 1:1 매핑한다.

```jsx
// map 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스 ,this) 인수 전달.
[1, 2, 3].map((item,index,arr) => {
	console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
	return item;
});
// 요소값 : 1 인덱스 : 0 this: [1,2,3]
// 요소값 : 2 인덱스 : 1 this: [1,2,3]
// 요소값 : 3 인덱스 : 2 this: [1,2,3]
```

</aside>

### **📌 27.9.4 Array.prototype.filter**

<aside>
🍁

→ filter 메서드는 자신을 호출한 배열의 모든 요소를 순회하면 인수로 전달받은 콜백 함수를 반복 호출한다.

- 원본 배열은 변경되지 않는다.
- 콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환한다.

```jsx
const numbers = [1, 2, 3, 4, 5];

// filter 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 호출
// 콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환한다.
// numbers 배열에서 홀수인 요소만 필터링한다(1은 true)
const odds = numbers.filter(item => item % 2);
console.log(odds); // [1, 3, 5]
```

→ filter 메서드는 자신을 호출한 배열에서 조건을 만족하는 특정 요소만 추출하여 새로운 배열을 만들고 싶을 때 사용한다.

- 위 예제에서는 2로 나눈 나머지를 반환한다.
- 이때 반환값이 true인 홀수인 요소만 추출하여 새로운 배열을 반환한다.
- filter 메서드가 생성하여 반환한 새로운 배열의 length 프로퍼티 값은 filter 메서드를 호출한 배열의 length 프로퍼티 값과 같거나 작다.

```jsx
// filter 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this) 인수 전달.
[1, 2, 3].filter((item, index, arr) => {
	console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
	return item % 2;
});
// 요소값 : 1 인덱스 : 0 this: [1,2,3]
// 요소값 : 2 인덱스 : 1 this: [1,2,3]
// 요소값 : 3 인덱스 : 2 this: [1,2,3]
```

</aside>

### **📌 27.9.5 Array.prototype.reduce**

<aside>
🍁

→ reduce 메서드는 자신을 호출한 배열을 모든 요소를 순회하며 인수로 전달받은 콜백 함수를 반복 호출한다.

- 콜백 함수의 반환값을 다음 순회 시에 콜백 함수의 첫 번째 인수로 전달하면서 콜백 함수를 호출하여 하나의 결과값을 만들어 반환한다.
- 원본 배열은 변경되지 않는다.

→ reduce 인수

1. 첫 번째 인수로 콜백 함수
2. 두 번째 인수로 초기값을 전달받는다.
3. 반환하는 콜백 함수에는 4개의 인수를 갖는다.

```jsx
// 1부터 4까지 누적을 구한다.
const sum = [1, 2, 3, 4].reduce((accumulator, currentValue, index, array) =>
acumulator + currentValue, 0);
console.log(sum); // 10
```

→ 콜백 함수의 4가지 인수

1. 초기값
2. 콜백 함수의 이전 반환값
3. reduce 메서드를 호출한 배열의 요소값과 인덱스
4. reduce 메서드를 호출한 배열자체 ⇒ this

→ 예제로 이해하기

1. 평균 구하기

```jsx
const values = [1, 2, 3, 4, 5, 6];
const average = values.reduce(( acc, cur, i, { length }) => {
	// 마지막 순회가 아니면 누적값을 반환하고 마지막 순회면 누적값으로 평균 반환
	return i === length - 1 ? (acc + cur) / length : acc + cur;
}, 0);
console.log(average); // 3.5
```

1. 최대값 구하기

```jsx
const values = [1, 2, 3, 4, 5];
const max = values.reduce((acc,cur) => (acc > cur ? acc : cur), 0);
console.log(max); // 5
```

</aside>

### **📌 27.9.6 Array.prototype.some**

<aside>
🍁

→ some 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다.

- some 메서드는 콜백 함수의 반환값이 단 한번이라도 참이면, true 모두 거짓이면 false를 반환한다.
- 콜백 함수를 통해 정의한 조건을 만족하는 요소가 1개 이상 존재하는지 확인하여 결과를 불리언 타입으로 반환한다.
- some 메서드를 호출한 배열이 빈 배열인 경우 언제나 false를 반환한다.

```jsx
// 배열의 요소 중 10보다 큰 요소가 1개 이상 존재하는지 확인
[5, 10 ,15].some(item => itme > 10); // -> true
// 배열의 요소 중 0보다 작은 요소가 1개 이상 존재하는지 확인
[5, 10, 15].some(item => item < 0); // -> false
// 배열 요소 중 'banana'가 1개 이상 존재하는지 확인
['apple', 'banana', 'mango'].some(item => item === 'banana'); // -> true
// some 메서드를 호출한 배열이 빈 배열인 경우 언제나 false를 반환
[].some(item => item > 3); // -> false
```

</aside>

### **📌 27.9.7 Array.prototype.every**

<aside>
🍁

→ every 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다.

- every 메서드는 콜백 함수의 반환값이 모두 참이면 true, 단 한번이라도 거짓이면 false 반환한다.
- 배열의 모든 요소가 콜백 함수를 통해 정의한 조건을 모두 만족하는지 확인하여 결과를 불리언 타입으로 반환한다.
- every 메서드를 호출한 배열이 빈 배열인 경우 언제나 true를 반환한다.

```jsx
// 배열의 모든 요소가 3보다 큰지 확인
[5, 10, 15].every(item => item > 3); // -> true
// 배열의 모든 요소가 10보다 큰지 확인
[5, 10 ,15].every(item => item > 10); // -> false
// every 메서드를 호출한 배열이 빈 배열인 경우 언제나 true
[].every(item => item > 3); // -> true
```

</aside>

### **📌 27.9.8 Array.prototype.find**

<aside>
🍁

→ ES6에서 도입된 find 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫 번째 요소를 반환한다.

- 콜백 함수의 반환 값이 true인 요소가 존재하지 않는다면 undefined를 반환한다.

```jsx
const users = [
	{ id: 1, name: 'Lee' },
	{ id: 2, name: 'Kim' },
	{ id: 3, name: 'Choi' },
	{ id: 4, name: 'Park' },
];
// id가 2인 첫 번째 요소를 반환한다.
users.find(user => user.id === 2); // -> {id: 2, name: 'Kim'}
```

</aside>

### **📌 27.9.9 Array.prototype.findIndex**

<aside>
🍁

→ ES6에서 도입된 findIndex 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫 번째 요소의 인덱스를 반환한다.

- 콜백 함수를 호출하여 반환값이 true 인 첫번 째 요소를 반환한다.
- 콜백 함수의 반환값이 true인 요소가 존재하지 않는다면 -1을 반환한다.

```jsx
const users = [
	{ id: 1, name: 'Lee' },
	{ id: 2, name: 'Kim' },
	{ id: 3, name: 'Choi' },
	{ id: 4, name: 'Park' },
];
// id가 2인 첫 번째 요소를 반환한다.
users.findIndex(user => user.id === 2); // -> 1
// name이 'Park'인 요소의 인덱스를 구한다.
users.findIndex(user => user.name === 'Park'); // -> 3
// 위와 같이 프로퍼티 키와 프로퍼티 값으로 요소의 인덱스를 구할 시
// 콜백함수 제작하기
function predicate(key, value) {
	// key 와 value을 기억하는 클로저를 반환
	return item => item[key] === value;
}

// id가 2인 요소의 인덱스를 구한다
users.findIndex(predicate('id', 2)); // -> 1
// name이 Park인 요소의 인덱스를 구한다
users.findIndex(predicate('name', 'Park')); // -> 3
```

</aside>

### **📌 27.9.10 Array.prototype.flatMap**

<aside>
🍁

→ ES10 에서 도입된 flatMap 메서드는 map 메서드를 통해 생성된 새로운 배열을 평탄화한다.

- map 메서드와 flat 메서드를 순차적으로 실행하는 효과가 있다.

```jsx
const arr = ['hello', 'world'];
// map과 flat을 순차적으로 실행 
arr.map(x => x.split('')).flat();
// -> ['h', 'e', 'l', 'l', 'o', 'w', 'o;, 'r', 'l', 'd']

// flatmap은 map을 통해 생성된 새로운 배열을 평탄화 한다.
arr.flatMap(x => x.split(''));
// -> ['h', 'e', 'l', 'l', 'o', 'w', 'o;, 'r', 'l', 'd']
```

</aside>