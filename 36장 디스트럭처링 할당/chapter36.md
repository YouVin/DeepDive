### ⭐️36.1 배열 디스트럭처링 할당

<aside>
🐛

→ ES5에서 구조화된 배열을 디스트럭처링 하여 1개 이상의 변수에 할당하는 방법은 다음과 같다.

```jsx
// ES5
var arr = [1, 2, 3];

var one = arr[0]; 
var two = arr[1];
var three = arr[2];

console.log(one, two, three); // 1 2 3
```

→ ES6의 배열 디스트럭처링 할당은 배열의 각 요소를 배열로부터 추출하여 1개 이상의 변수에 할당한다.

- 배열 디스트럭처링 할당의 대상은 이터러블이어야 하며, 할당 기준은 배열의 인덱스다.

```jsx
const arr = [1, 2, 3];

// ES6 배열 디스트럭처링 할당
// 변수 one, two, three를 선언하고 배열 arr을 디스트럭처링하여 할당
// 이때 할당 기준은 배열의 인덱스다.
const [one, two, three] = arr;

console.log(one, two, three); // 1 2 3

// 1. 배열 디스트럭처링 할당을 위해서는 왼쪽에 할당받을 변수를 선언한다.
// 이때 변수를 배열 리터럴 형태로 선언한다.
const [x, y] = [1, 2];
// 만약 우변에 이터러블을 할당하지 않으면?
const [x, y]; // SyntaxError
const [a, b] = {}; // TypeError

// 2. 배열 디스트럭처링 할당의 변수 선언문은 다음과 같이 분리도 가능하지만, 권장안함
let x, y;
[x,y] = [1, 2]; // 권장안함.

// 3. 배열 디스트럭처링 할당의 기준은 배열의 인덱스다.
// 변수의 개수와 이터러블의 요소 개수가 반드시 일치할 필요는 없다.
const [a, b] = [1, 2];
console.log(a, b); // 1 2

 const [c, d] = [1];
 console.log(c, d); // 1 undefined
 
 const [e, f] = [1, 2, 3];
 console.log(e, f); // 1 2
 
 // 4. 배열 디스트럭처링 할당을 위한 변수에 기본값을 설정할 수 있다.
 // 기본값
 const [a, b, c = 3] = [1, 2];
 console.log(a, b, c); // 1 2 3
 
 // 기본값보다 할당된 값이 우선한다.
 const [e, f = 10, g = 3] = [1, 2];
 console.log(e, f, g); // 1 2 3
```

→ 배열 디스트럭처링 예제

- URL을 파싱하여 protocol, host, path 프로퍼티를 갖는 객체를 생성해 반환한다.

```jsx
// url을 파싱하여 protocol, host, path 프로퍼티를 갖는 객체를 생성해 반환한다.
function parseURL(url = '') {
	// '://' 앞의 문자열(protocol)과 '/' 이전의 '/'로 시작하지 않는 문자열(host)과
	// '/' 이후의 문자열(path)를 검색한다.
	const parsedURL = url.match(/^(\w+):/\/\([^/]+)\/(.*$/);
	console.log(parsedURL); 

	if (!parsedURL) return {};
	
	// 배열 디스트럭처링 할당을 사용하여 이러터블에서 필요한 요소만 추출한다.
	const [, protocol, host, path] = parsedURL;
	return { protocol, host, path };
}

const parsedURL = parseURL('https://developer.mozilla.org/ko/docs/Web/Java');
console.log(parsedURL);
// prtocol: 'https',
// host: 'developer.mozilla.org,
// path: 'ko/docs/Web/Java'
```

</aside>

### ⭐️36.2 객체 디스트럭처링 할당

<aside>
🐛

→ ES5에서 객체의 각 프로퍼티를 객체로부터 디스트럭처링하여 변수에 할당하기 위해서는 프로퍼티를 사용해야 한다.

```jsx
// ES5
var user = { firstName: 'Ungmo', lastName: 'Lee' };

var firstName = user.firstName;
var lastName = user.lastName;

console.log(firstName, lastName); // Ungmo Lee
```

→ ES6의 객체 디스트럭처링 할당은 객체의 각 프로퍼티를 객체로부터 추출하여 1개 이상의 변수에 할당한다.

- 객체 디스트럭처링 할당의 대상은 객체이어야 하며, 할당 기준은 프로퍼티 키다.
- 순서는 의미가 없으며 선언된 변수 이름과 프로퍼티 키가 일치하면 할당된다.

```jsx
const user = { firstNmae: 'Ungmo', lastName: 'Lee' };

// ES6 객체 디스트럭처링 할당
// 변수 lastName, firstName을 선언하고 user 객체를 디스트럭처링하여 할당한다.
// 이때 프로퍼티 키를 기준으로 디스트럭처링 할당이 이루어진다. 순서는 의미 X
const { lastName, firstName } = user;
console.log(firstName, lastName); // Ungmo Lee

// 1. 객체 디스트럭처링 할당을 위해서는 할당 연산자 왼쪽에 프로퍼티 값을 할당
// 받을 변수를 선언하고, 객체 리터럴 형태로 선언한다.
const { lastName, firstName } = { firstName: 'Ungmo', lastName: 'Lee' };

// 2. 우변에 객체 또는 평가될 수 있는 표현식을 할당하지 않으면 에러 발생.
const { lastName, firstName }; // SyntaxError
const { lastName, firstName } = null; // TypeError

// 3. 객체의 프로퍼티 키와 다른 변수 이름으로 프로퍼티 값을 할당 받으려면 변수 선언
const user = { fistName: 'Ungmo', lastName: 'Lee' };

// 프로퍼티 키를 기준으로 디스트럭처링 할당이 이루어진다.
// 프로퍼티 키가 lastName인 프로퍼티 값을 ln에 할당하고,
// 프로퍼티 키가 firstName인 프로퍼티 값을 fn에 할당한다.
const { lastName: ln, fistName: fn } = user;
console.log(fn, ln); // Ungmo Lee

// 4. 객체 디스트럭처링 할당을 위한 변수에 기본값 설정이 가능하다.
const { firstName = 'Umgmo', lastNmae } = { lastName: 'Lee' };
console.log(firstName, lastName); // Ungmo Lee

const { firstName: fn = 'Ungmo', lastName: ln } = { lastName: 'Lee'};
console.log(fn, ln); // Ungmo Lee
```

→ 객체 디스트럭처링 할당은 객체에서 프로퍼티 킬로 필요한 프로퍼티 값만 추출하여 변수에 할당하고 싶을 때 유용하다.

```jsx
const str = 'Hello';
// String 래퍼 객체로부터 length 프로퍼티만 추출한다.
const { length } = str;
console.log(length); // 5

const todo = { id: 1, content: 'HTML', completed: true };
// todo 객체로부터 id 프로퍼티만 추출한다.
const { id } = todo;
console.log(id); // 1

// 객체 디스트럭처링 할당은 객체를 인수로 전달받는 함수의 매개변수에도 사용 가능
function printTodo(todo) {
	console.log(`할일 ${todo.content}은 ${todo.completed ? '완료' : '비완료'} 상태
	입니다.`);
}
printTodo({id:1, content: 'HTML', completed: true}); // 할일 HTML은 완료 상태
```

→ 배열의 요소가 객체인 경우 배열 디스트럭처링 할당과 객체 디스트럭처링 할당을 혼용할 수 있다.

```jsx
const todos = [
	{ id: 1, content: 'HTML', completed: true },
	{ id: 2, content: 'CSS', completed: false },
	{ id: 3, content: 'JS', completed: false }
];

// todos 배열의 두 번째 요소인 객체로부터 id 프로퍼티만 추출한다.
const [, { id }] = todos;
console.log(id); // 2

// 중첩 객체의 경우는?
const user = {
	name: 'Lee',
	address: {
		zipCode: '03068',
		city: 'Seoul'
	}
};

// address 프로퍼티 키로 객체를 추출하고 이 객체의 city 프로퍼티 키로 추출한다.
const { address: { city } } = user;
console.log(city); // 'Seoul'
```

</aside>