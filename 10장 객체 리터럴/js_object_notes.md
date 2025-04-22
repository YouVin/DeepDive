
### ⭐️객체란?

- 자바스크립트는 객체 기반의 프로그래밍 언어이며, 자바스크립트를 구성하는 거의 “모든 것”이 객체다.
- 원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식)은 모두 객체다.
- 원시 타입 → 단 하나의 값 , 객체 타입 → 다양한 타입의 값
- 원시 타입의 값 → 변경 불가능한 값, 객체 타입의 값 → 변경 가능한 값
- 객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키(key)와 값(value)으로 구성된다.

`var person = { key : ‘값’ }` 

→ 객체는 프로퍼티의 집합 

→ 객체의 프로퍼티의 메서드

→ 객체 = 프로퍼티 + 메서드로 구성된 집합체 ,  프로퍼티와 메서드의 역할

- 프로퍼티 : 객체의 상태를 나타내는 값
- 메서드 : 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작

→ 객체는 객체의 상태를 나타내느 값과 프로퍼티를 참조하고 조작할 수 있는 동작을 모두 포함할 수 있기 때문에 상태와 동작을 하나의 단위로 구조화할 수 있어 유용하다.

### ⭐️객체 리터럴에 의한 객체 생성

#### 🔑 인스턴스 Instance

- 클래스 - 객체 생성을 위한 설계도
- 객체 - 만들어진 데이터 덩어리
- 인스턴스 - 클래스 기반으로 생성된 특정 객체

```jsx
class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(`${this.name}가 소리를 낸다!`);
  }
}
const dog1 = { name: "멍멍이" };
const dog = new Animal("멍멍이");
const cat = new Animal("야옹이");

dog.speak();
cat.speak();

console.log(dog1 instanceof Animal); // false
console.log(dog instanceof Animal);  // true
```

## 💡 개념 정리

| 개념 | 정의 | 예시 |
| --- | --- | --- |
| **클래스** | 객체 생성을 위한 **청사진, 설계도** | `class Animal { ... }` |
| **객체** | 실제로 만들어진 **데이터 덩어리** | `const dog = new Animal("멍멍이")` |
| **인스턴스** | 클래스 기반으로 생성된 **특정 객체** | `dog`, `cat`은 `Animal` 클래스의 인스턴스 |

### 😛 객체 생성 방법

```jsx
var person = {
  name: 'Lee',
  sayHello: function(){
    console.log(`Hello/ My name is ${this.name}`);
  }
};
```

```jsx
var empty = {};
```

> **중괄호가 객체 리터럴이면 "값" → 세미콜론 붙이기!**  
> **중괄호가 코드 블록이면 "범위" → 세미콜론 안 붙이기!**

### ⭐️프로퍼티

- 프로퍼티 키는 문자열 또는 심벌, 값은 모든 값 가능
- 키가 문법 규칙 어기면 따옴표 필요

```jsx
const person = {
  name: "유빈",
  age: 20,
  "full name": "황유빈",
  "1stPlace": "숨참고딥다이브"
};
const mySymbol = Symbol("secret");
const obj = { [mySymbol]: "비밀이에요" };
```

#### 계산된 프로퍼티 이름 (ES5 vs ES6)

```js
// ES5
var obj = {};
var key = 'hello';
obj[key] = 'world';

// ES6
var key = 'hello';
var obj = { [key]: 'world' };
```

```js
var foo = { 
  0: 1,
  1: 2,
  2: 3
};
```

### ⭐️메서드

```js
var circle = {
  radius : 5,
  getDiameter: function(){
    return 2 * this.radius;
  }
};
```

### ⭐️프로퍼티 접근

```js
var person = {
  name: 'Lee',
  'last-name': 'Dee',
  1: 10
};
console.log(person.name); // 마침표
console.log(person["last-name"]); // 대괄호
console.log(person[1]); // 숫자
```

### ⭐️프로퍼티 값 갱신

```js
var person = { name: 'Lee' };
person.name = 'Kim';
```

### ⭐️프로퍼티 동적 생성

```js
var person = { name: 'Lee' };
person.age = 20;
```

### ⭐️프로퍼티 삭제

```js
var person = { name: 'Lee' };
delete person.age;
delete person.address;
```

### ⭐️ES6 객체 리터럴의 확장 기능

#### 📌 프로퍼티 축약 표현

```js
// ES5
var x = 1, y = 2;
var obj = { x: x, y: y };

// ES6
let x = 1, y = 2;
const obj = { x, y };
```

#### 📌 계산된 프로퍼티 이름

```js
// ES5
var prefix = 'prop', i = 0, obj = {};
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;

// ES6
const prefix = 'prop';
let i = 0;
const obj = {
  [`${prefix} - ${++i}`]: i,
  [`${prefix} - ${++i}`]: i,
  [`${prefix} - ${++i}`]: i
};
```

#### 📌 메서드 축약 표현

```js
// ES5
var obj = {
  name: 'Lee',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

// ES6
const obj = {
  name: 'Lee',
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};
```
