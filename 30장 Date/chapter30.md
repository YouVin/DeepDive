### ⭐️30 Date

<aside>
🍀

→ 표준 빌트인 객체 Date는 날짜와 시간을 위한 메서드를 제공하는 빌트인 객체이면서 생성자 함수이다.

- UTC는 국제 표준시
- KST는 한국 표준시
- 현재 날짜와 시간은 자바스크립트 코드가 실행된 시스템의 시계에 의해 결정된다.
</aside>

### ⭐️30.1 Date 생성자 함수

<aside>
🍀

→ Date는 생성자 함수다.

- Date 객체는 내부적으로 날짜와 시간을 나타내는 정수값을 갖는다.
- 값은 1970년 1월 1일 기점으로 Date 객체가 나타내는 날짜와 시간까지의 밀리초를 나타낸다.
</aside>

### **📌 30.1.1 new Date()**

<aside>
🍀

→ Date 생성자 함수를 인수없이 new 연산자와 함께 호출하면 현재 날짜와 시간을 가지는 Date객체를 반환한다.

- Date 객체는 내부적으로 날짜와 시간을 나타내는 정수값을 갖지만 Date 객체를 콘솔에 출력하면 기본적으로 날짜와 시간 정보를 출력한다.
- `new Date();` // → Mon Jul 06 2020 01:03:18 GMT+0900
- `Date()`  // → Mon Jul 06 2020 01:03:18 GMT+0900
</aside>

### **📌 30.1.2 new Date(milliseconds)**

<aside>
🍀

→ Date 생성자 함수에 숫자 타입의 밀리초를 인수로 전달하면 1970년 1월 1일 00:00:00(UTC) 기점으로 인수로 전달된 밀리초만큼 경과한 날짜와 시간을 나타내는 Date 객체를 반환한다.

```jsx
// 한국 표준시 KST는 협정 세계시 UTC에 9시간을 더한 시간
new Date();  // → Mon Jul 06 2020 01:03:18 GMT+0900

new Date(86400000) // 1day 이후 
```

</aside>

### **📌 30.1.3 new Date(dateString)**

<aside>
🍀

→ Date 생성자 함수에 날짜와 시간을 나타내는 문자열을 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date 객체를 반환한다.

```jsx
new Date('May 26, 2020 10:00:00');
// Tue May 26 2020 10:00:00 GMT+0900

new Date('2020/03/26/10:00:00');
// Tue May 26 2020 10:00:00 GMT+0900
```

</aside>

### **📌 30.1.4 new Date(year, month[, day, hour, minute, second, millisecond])**

<aside>
🍀

→ Date 생성자 함수에 연, 월, 일, 시, 분, 초, 밀리초를 의미하는 숫자를 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date객체를 반환한다.

| 인수 | 내용 |
| --- | --- |
| year | 연을 나타내는 1900년 이후의 정수 |
| month | 월을 나타내는 0~11까지의 정수 |
| day | 일을 나타내는 1~31까지의 정수 |
| hour | 시를 나타내는 0~23까지의 정수 |
| minute | 분을 나타내는 0~59까지의 정수 |
| second | 초를 나타내는 0~59까지의 정수 |
| millisecond | 밀리초를 나타내는 0~999까지의 정수 |
</aside>

### ⭐️30.2 Date 메서드

### **📌 30.2.1 Date.now**

<aside>
🍀

→ 1970년 1월 1일 00:00:00(UTC)을 기점으로 현재 시간까지 경과한 숫자를 밀리초로 반환한다.

`Date.now();` → 159393591239

</aside>

### **📌 30.2.2 Date.parse**

<aside>
🍀

→ 1970년 1월 1일 00:00:00을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환

```jsx
// UTC
Date.parse('Jan 2, 1970 00:00:00 UTC'); // -> 86400000

// KST
Date.parse('Jan 2, 1970 09:00:00');  // -> 86400000

// KST
Date.parse('1970/01/02/09:00:00');  // -> 86400000
```

</aside>

### **📌 30.2.3 Date.UTC**

<aside>
🍀

→ 1970년 1월 1일 00:00:00을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환

- new Date와 같은 형식의 인수를 사용해야 한다.

```jsx
Date.UTC(1970, 0, 2); // -> 86400000
Date.UTC('1970/1/2'); // -> NaN
```

</aside>

### **📌 30.2.4 Date.prototype.getFullYear**

<aside>
🍀

→ Date 객체의 연도를 나타내는 정수를 반환

`new Date(’2020/07/24’).getFullYear();` // → 2020

</aside>

### **📌 30.2.5 Date.prototype.setFullYear**

<aside>
🍀

→ Date 객체에 연도를 나타내는 정수를 설정한다.

- 연도 이외에 옵션으로 월, 일도 설정할 수 있다.

```jsx
const today = new Date();
// 년도 지정
today.setFullYear(2000); 
today.getFullYear(); // 2000
// 년도/월/일 지정
today.setFullYear(1900, 0 , 1); 
today.getFullYear(); // 1900
```

</aside>

### **📌 30.2.6 Date.prototype.getMonth**

<aside>
🍀

→ Date 객체의 월을 나타내는 0~11의 정수를 반환한다. 1월은 0 12월은 11이다.

`new Date(’2020/07/24’).getMonth();` // 6

</aside>

### **📌 30.2.7 Date.prototype.setMonth**

<aside>
🍀

→ Date 객체에 월을 나타내는 0~11의 정수를 설정한다. 월 이외에 옵션으로 일도 설정할 수 있다.

```jsx
const today = new Date();

// 월 지정
today.setMonth(0); // 1월
today.getMonth(); // 0

// 월/일 지정
today.setMonth(11, 1); // 12월 1일
today.getMonth(); // 11
```

</aside>

### **📌 30.2.8 Date.prototype.getDate**

<aside>
🍀

→ Date 객체의 날짜(1~31)를 나타내는 정수를 반환한다.

`new Date(’2020/07/24’).getDate();` // → 24

</aside>

### **📌 30.2.9 Date.prototype.setDate**

<aside>
🍀

→ Date 객체에 날짜(1~31)를 나타내는 정수를 설정한다.

```jsx
const today = new Date();

// 날짜 지정
today.setDate(1);
today.getData(); // -> 1
```

</aside>

### **📌 30.2.10 Date.prototype.getDay**

<aside>
🍀

→ Date 객체의 요일(0~6)을 나타내는 정수를 반환한다. 반환값은 다음과 같다.

| 요일 | 반환값 |
| --- | --- |
| 일요일 | 0 |
| 월요일 | 1 |
| 화요일 | 2 |
| 수요일 | 3 |
| 목요일 | 4 |
| 금요일 | 5 |
| 토요일 | 6 |

`new Date(’2020/07/24’).getDay();` // → 5

</aside>

### **📌 30.2.11 Date.prototype.getHours**

<aside>
🍀

→ Date 객체의 시간(0~23)을 나타내는 정수를 반환한다.

`new Date(’2020/07/24/12:00’).getHours();` // → 12

</aside>

### **📌 30.2.12 Date.prototype.setHours**

<aside>
🍀

→ Date 개게에 시간(0~23)을 나타내는 정수를 설정한다.

- 시간 이외에 옵션으로 분, 초, 밀리초도 설정할 수 있다.

```jsx
const today = new Date();

// 시간지정
today.setHours(7);
today.getHours(); // -> 7

// 시간/분/초/밀리초 지정
today.setHours(0, 0, 0, 0); // 00:00:00:00
today.getHours(); // -> 0
```

</aside>

### **📌 30.2.13 Date.prototype.getMinutes**

<aside>
🍀

→ Date 객체의 분(0~59)을 나타내는 정수를 반환한다.

`new Date(’2020/07/24/12:30’).getMinutes();` // → 30

</aside>

### **📌 30.2.14 Date.prototype.setMinutes**

<aside>
🍀

→ Date 객체에 분(0~59)을 나타내는 정수를 설정한다.

- 분 이외에 옵션으로 초, 밀리초도 설정할 수 있다.

```jsx
const today = new Date();

// 시간지정
today.**setMinutes**(50);
today.**setMinutes**(); // -> 50

// 시간/분/초/밀리초 지정
today.**setMinutes**(5, 10, 999); // HH:05:10:999
today.**setMinutes**(); // -> 5
```

</aside>

### **📌 30.2.15 Date.prototype.getSeconds**

<aside>
🍀

→ Date 객체의 초(0 ~ 59)를 나타내는 정수를 반환한다.

`new Date(’2020/07/24/12:30:10’).getSecond();` // → 10

</aside>

### **📌 30.2.16 Date.prototype.setSeconds**

<aside>
🍀

→ Date 객체에 초(0~59)를 나타내는 정수를 설정한다.

- 초 이외에 옵션으로 밀리초도 설정할 수 있다.

```jsx
const today = new Date();

// 시간지정
today.**setSeconds**(30);
today.**setSeconds**(); // -> 30

// 시간/분/초/밀리초 지정
today.**setSeconds**(10, 0); // HH:MM:10:000
today.**setSeconds**(); // -> 10
```

</aside>

### **📌 30.2.17 Date.prototype.getMillisecond**

<aside>
🍀

→ Date 객체에 밀리초(0~999)를 나타내는 정수를 반환한다.

`new Date(’2020/07/24/12:30:10:150’).getMilliseond();` // → 150

</aside>

### **📌 30.2.18 Date.prototype.setMilliseconds**

<aside>
🍀

→  Date 객체에 밀리초(0~999)를 나타내는 정수를 설정한다.

```jsx
const today = new Date();

// 밀리초 지정
today.**setMilliseconds**(123);
today.**setMilliseconds**(); // -> 123
```

</aside>

### **📌 30.2.19 Date.prototype.getTime**

<aside>
🍀

→ 1970년 1월 1일 00:00:00(UTC)를 기점으로 Date 객체의 시간까지 경과된 밀리초를 반환한다.

`new Date(’2020/07/24/12:30’).getTime();` // → 159556140000

</aside>

### **📌 30.2.20 Date.prototype.setTime**

<aside>
🍀

→ Date 객체에 1970년 1월 1일 00:00:00(UTC)를 기점으로 경과된 밀리초를 설정한다.

```jsx
const today = new Date();

// 밀리초 지정
today.**setTime**(86400000);
console.log(today); // Fri Jan 02 1970 09:00:00 GMT+0900
```

</aside>

### **📌 30.2.21 Date.prototype.getTimezoneOffset**

<aside>
🍀

→ UTC와 Date 객체에 지정된 로컬시간과의 차이를 분 단위로 반화난다.

```jsx
const today = new Date();

// UCT와 today의지정 로컬 KST 차이는 -9시간이다.
today.**getTimezoneOffset() / 60; // -9**
```

</aside>

### **📌 30.2.22 Date.prototype.toDateString**

<aside>
🍀

→ 사람이 읽을 수 있는 형식의 문자열로 Date 객체의 날짜를 반환한다.

```jsx
const today = new Date();

today.toString**(); // Fri Jul 24 2020 12:30:00 GMT+0900
today.toDateString(); // Fri Jul 24 2020**
```

</aside>

### **📌 30.2.23 Date.prototype.toTimeString**

<aside>
🍀

→ 사람이 읽을 수 있는 형식으로 Date 객체의 시간을 표현한 문자열을 반환한다.

```jsx
const today = new Date();

today.toString**(); // Fri Jul 24 2020 12:30:00 GMT+0900
today.toTimeString(); // 12:30:00 GMT+0900**
```

</aside>

### **📌 30.2.24 Date.prototype.toISOString**

<aside>
🍀

→ ISO 8601 형식으로 Date 객체의 날짜와 시간을 표현한 문자열을 반환한다.

```jsx
const today = new Date('2020/7/24/12:30');

today.toString();  // Fri Jul 24 2020 12:30:00 GMT+0900
today.toISOString(); // 2020-07-24T03:30:00.000Z
```

</aside>

### **📌 30.2.25 Date.prototype.toLocaleString**

<aside>
🍀

→ 인수로 전달한 로컬을 기준으로 Date 객체의 날짜와 시간을 표현한 문자열을 반환한다.

- 인수를 생략한 경우 브라우저가 동작 중인 시스템의 로컬을 적용한다.

```jsx
const today = new Date('2020/7/24/12:30');

today.toString();  // Fri Jul 24 2020 12:30:00 GMT+0900
today.**toLocaleString**(); // 2020. 7. 24. 오후 12:30:00
today.**toLocaleString**('ko-KR'); // 2020. 7. 24. 오후 12:30:00
today.**toLocaleString**('en-US'); // 7/24/2020. 12:30:00 PM
today.**toLocaleString**('ja-JP'); // 2020/7/24 12:30:00
```

</aside>

### **📌 30.2.26 Date.prototype.toLocalTimeString**

<aside>
🍀

→ 인수로 전달한 로컬을 기준으로 Date 객체의 시간을 표현한 문자열을 반환한다

- 인수를 생략한경우 브라우저가 동작 중인 시스템의 로컬을 적용한다.

```jsx
const today = new Date('2020/7/24/12:30');

today.toString();  // Fri Jul 24 2020 12:30:00 GMT+0900
today.**toLocaleString**(); // 오후 12:30:00
today.**toLocaleString**('ko-KR'); // 오후 12:30:00
today.**toLocaleString**('en-US'); // 12:30:00 PM
today.**toLocaleString**('ja-JP'); // 12:30:00
```

</aside>