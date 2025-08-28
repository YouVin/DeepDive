### ⭐️29.1 Math 프로퍼티

### **📌 29.1.1 Math.PI**

<aside>
🔑

→ 원주율 PI 값을 반환한다.

`Math.PI;`  → 3.1415926535…

</aside>

### ⭐️29.2 Math 메서드

### **📌 29.2.1 Math.abs**

<aside>
🔑

→ Math.abs 메서드는 인수로 전달된 숫자의 절대값을 반환한다.

- 절대값은 반드시 0 또는 양수이어야 한다.

```jsx
Math.abs(-1); // -> 1
Math.abs('-1'); // -> 1
Math.abs(''); // -> 0
Math.abs([]); // -> 0
Math.abs(null); // -> 0
Math.abs(undefined); // -> NaN
Math.abs({}); // -> NaN
Math.abs('string'); // -> NaN
Math.abs(); //-> NaN
```

</aside>

### **📌 29.2.2 Math.round**

<aside>
🔑

→ Math.round 메서드는 인수로 전달된 숫자의 소수점 이하를 반올림한 정수를 반환한다.

```jsx
Math.round(1.4); // -> 1
Math.round(1.6); // -> 2
Math.round(-1.4); // -> -1
Math.round(-1.6); // -> -2
Math.round(1); // -> 1
Math.round(); // -> NaN
```

</aside>

### **📌 29.2.3 Math.ceil**

<aside>
🔑

→ Math.ceil 메서드는 인수로 전달된 숫자의 소수점 이하를 올림한 정수를 반환한다.

- 소수점 이하를 올림하면 더 큰 정수가 된다.

```jsx
Math.ceil(1.4); // -> 2
Math.ceil(1.6); // -> 2
Math.ceil(-1.4); // -> -1
Math.ceil(-1.6); // -> -1
Math.ceil(1); // -> 1
Math.ceil(); // -> NaN
```

</aside>

### **📌 29.2.4 Math.floor**

<aside>
🔑

→ Math.floor 메서드는 인수로 전달된 숫자의 소주점 이하를 내림한 정수를 반환한다.

- Math.ceil의 반대 개념이다.

```jsx
Math.floor(1.9); // -> 1
Math.floor(9.1); // -> 9
Math.floor(-1.9); // -> -2
Math.floor(-9.1); // -> -10
Math.floor(1); // -> 1
Math.floor(); // -> NaN
```

</aside>

### **📌 29.2.5 Math.sqrt**

<aside>
🔑

→ Math.sqrt 메서드는 인수로 전달된 숫자의 제곱근을 반환한다.

```jsx
Math.sqrt(9); // -> 3
Math.sqrt(-9); // -> NaN
Math.sqrt(2); // -> 1.414213562...
Math.sqrt(1); // -> 1
Math.sqrt(0); // -> 0
Math.sqrt(); // -> NaN
```

</aside>

### **📌 29.2.6 Math.random**

<aside>
🔑

→ Math.random 메서드는 임의의 난수를 반환한다.

- Math.random 메서드가 반환한 난수는 0에서 1 미만의 실수다.
- 0은 포함되지만 1은 포함되지 않는다.

```jsx
Math.random(); // 0에서 1미만의 랜덤 실수
const random = Math.floor((Math.random() * 10 ) + 1);
console.log(random); // 1에서 10 범위의 정수
```

</aside>

### **📌 29.2.7 Math.pow**

<aside>
🔑

→ Math.pow 메서드는 첫 번째 인수를 밑으로, 두번째 인수를 지수로 거듭제곱한 결과를 반환한다.

```jsx
Math.pow(2, 8); // -> 256
Math.pow(2, -1); // -> 0.5
Math.pow(2); // -> NaN

// Math.pow 대신 ES8에서 도입된 지수 연산자 사용
2 ** 2 ** 2; // -> 16
```

</aside>

### **📌 29.2.8 Math.max**

<aside>
🔑

→ Math.max 메서드는 전달받은 인수 중에서 가장 큰 수를 반환한다.

- 인수가 전달되지 않으면 -Infinity를 반환한다.

```jsx
Math.max(1); // -> 1
Math.max(1, 2); // -> 2
Math.max(1, 2, 3); // -> 3
Math.max(); // -> -Infinity
```

</aside>

### **📌 29.2.9 Math.min**

<aside>
🔑

→ Math.min 메서드는 전달받은 인수 중에서 가장 작은 수를 반환한다.

- 인수가 전달되지 않으면 Infinity를 반환한다.

```jsx
Math.min(1); // -> 1
Math.min(1, 2); // -> 1
Math.min(1, 2, 3); // -> 1
Math.min(); // -> Infinity
```

</aside>