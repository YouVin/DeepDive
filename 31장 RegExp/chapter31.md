### ⭐️31.1 정규 표현식이란?

<aside>
🔅

→ 정규 표현식은 일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어다.

- 정규 표현식은 자바스크립트 고유 문법이 아니며, 대부분의 프로그래밍 언어와 코드 에디터에 내장되어 있다.
- 정규 표현식은 문자열을 대상으로 패턴 매칭 기능을 제공한다.
- 패턴 매칭 기능이란 특정 패턴과 일치하는 문자열을 검색하거나 추출 또는 치환하는 기능을 말한다.

```jsx
// 사용자로부터 입력받은 휴대폰 전화번호
const tel = '010-1234-567팔';

// 정규 표현식 리터럴로 휴대폰 전화번호 패턴을 정의한다.
const regExp = /^\d{3}-\d{4}-\d{4}$/;

// tel이 휴대폰 전화번호 패턴에 매칭하는지 테스트 한다.
regExp.test(tel); // -> false
```

</aside>

### ⭐️31.2 정규 표현식의 생성

<aside>
🔅

→ 정규 표현식 객체를 생성하기 위해서는 정규 표현식 리터럴과 RegExp 생성자 함수를 사용할 수 있다.

- 일반적인 방법은 정규 표현식 리터럴을 사용하는 것이다. /regexp/i
- 정규 표현식 리터럴은 패턴과 플래그로 구성된다.

```jsx
const target = 'Is this all there is?';

// 패턴: is
// 플래그: i => 대소문자를 구별하지 않고 검색한다.
const regexp = /is/i;

// test 메서드는 target 문자열에 대해 정규 표현식 regexp의 패턴을 검색하여 매칭
// 결과를 불리언 값으로 반환한다.
regexp.test(target); // -> true

// RegExp 생성자 함수로 생성하기
regexp2 = new RegExp(/is/i);  // ES6
regexp2.test(target); // -> true
```

</aside>

### ⭐️**31.3 RegExp 메서드**

### **📌 31.3.1 RegExp.prototype.exec**

<aside>
🔅

→ exec 메서드는 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 배열로 반환한다.

- 매칭 결과가 없는 경우 null을 반환한다.

```jsx
const target = 'Is this all there is?';
const regExp = /is/;

regExp.exec(target);
// -> ["is", index:5, input: "Is this all there is?", groups: undefined]
```

</aside>

### **📌 31.3.2 RegExp.prototype.test**

<aside>
🔅

→ test 메서드는 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 불리언 값으로 반환한다.

```jsx
const target = "Is this all there is?";
const regExp = /is/;

regExp.test(target); // -> true
```

</aside>

### **📌 31.3.3 String.prototype.match**

<aside>
🔅

→ String 표준 빌트인 객체가 제공하는 match 메서드는 대상 문자열과 인수로 전달받은 정규 표현식과 매칭 결과를 배열로 반환한다.

```jsx
const target = "Is this all there is?";
const regExp = /is/;

target.match(regExp);
// -> ["is", index:5, input: "Is this all there is?", groups: undefined]

regExp = /is/g;
target.match(regExp); // -> ["is", "is"]
```

</aside>

### ⭐️31.4 플래그

<aside>
🔅

→ 패턴과 함께 정규 표현식을 구성하는 플래그는 정규 표현식의 검색 방식을 설정하기 위해 사용한다.

| 플래그 | 의미  | 설명 |
| --- | --- | --- |
| i | ignore case | 대소문자를 구별하지 않고 패턴을 검색 |
| g  | Global | 대상 문자열 내에서 패턴과 일치하는 모든 문자열 전역 검색 |
| m  | Multi line | 문자열의 행이 바뀌더라도 패턴 검색을 계속한다. |
</aside>

### ⭐️31.5 패턴

<aside>
🔅

→ 정규 표현식은 “일정한 규칙”을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어다.

- 정규 표현식은 패턴과 플래그로 구성된다.
- 정규 표현식의 패턴은 문자열의 일정한 규칙을 표현하기 위해 사용하며, 정규 표현식의 플래그는 정규 표현식의 검색 방식을 설정하기 위해 사용한다.
- 패턴은 /로 열로 닫으며 문자열의 따옴표는 생략한다.
</aside>

### **📌 31.5.1 문자열 검색**

<aside>
🔅

→ 정규 표현식의 패턴에 문자 또는 문자열을 지정하면 검색 대상 문자열에서 패턴으로 지정한 문자 또는 문자열을 검색한다.

- 검색 대상 문자열과 플래그를 생략한 정규 표현식의 매칭 결과를 구하면 대소문자를 구별하여 정규 표현식과 매치한 첫 번째 결과만 반환한다.

```jsx
const target = 'Is this all there is?';

// 'is' 문자열과 매치하는 패턴. 플래그가 생략되었으므로 대소문자를 구별한다.
const regExp = /is/;

// target 과 정규 표현식이 매치하는지 테스트한다.
regExp.test(target); // -> true

// target과 정규 표현식의 매칭 결과를 구한다.
target.match(regExp);
// -> ["is", index: 5, input: "Is this all there is?", groups: undefined]

// 대소문자를 구별하지 않고 검색한다면 i 플래그를 추가
regExp = /is/i;
target.match(regExp);
// -> ["Is", index:0, input: "Is this all there is?", groups:undefined]

// 검색 대상 문자열 내에서 패턴과 매치하는 모든 문자열을 전역 검색하려면 g 플래그
regExp = /is/ig;
target.match(regExp);
// -> ["Is", "is", "is"]
```

</aside>

### **📌 31.5.2 임의의 문자열 검색**

<aside>
🔅

→ .은 임의의 문자 한 개를 의미한다.

- 문자의 내용은 무엇이든 상관없다.
- .을 3개 연속하여 패턴을 생성하면 문자의 내용과 상관없이 3자리 문자열과 매치한다.

```jsx
const target = "Is this all there is?";

// 임의의 3자리 문자열을 대소문자를 구별하여 전역 검색한다.
const regExp = /.../g;
target.match(regExp); // -> ["Is ", "thi", "s a", "the", "re ", "is?"]
```

</aside>

### **📌 31.5.3 반복 검색**

<aside>
🔅

→ {m, n}은 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열을 의미한다.

- 콤마 뒤에 공백이 있으면 정상 동작하지 않으므로 주의하기 바란다.

```jsx
const target = 'A AA B BB Aa Bb AAA';

// 'A' 가 최소 1번, 최대 2번 반복되는 문자열을 전역 검색한다.
const regExp = /A{1,2}/g
target.match(regExp); // -> ["A", "AA", "A", "AA", "A"]

// {n}은 앞선 패턴이 n번 반복되는 문자열을 의미한다. 즉 {n}은 {n,n}과 같다.
regExp = /A{2}/g;
target.match(regExp); // -> ["AA", "AA"]

// {n, }은 앞선 패턴이 최소 n번 이상 반복되는 문자열을 의미한다.
regExp = /A{2, }/g;
target.match(regExp); // -> ["AA", "AAA"]

// + 앞선 패턴이 최소 한번 이상 반복되는 문자열을 의미한다.
regExp = /A+/g;
target.match(regExp); // -> ["A", "AA", "A", "AAA"]

// ?는 앞선 패턴이 최대 한 번 이상 반복되는 문자열을 의미한다.
target = 'color colour';
regExp = /colou?r/g;
target.match(regExp); // -> ["color", "colour"]
```

</aside>

### **📌 31.5.4 OR 검색**

<aside>
🔅

→ |은 or의 의미를 갖는다.

```jsx
const target = 'A AA B BB Aa Bb';
// 'A' 또는 'B'를 전역 검색한다.
const regExp = /A|B/g;
target.match(regExp); // -> ["A", "A", "A", "B", "B", "B", "A", "B"]

// 분해되지 않은 단어 레벨로 검색하기 위해서는 +를 함께 사용한다.
regExp = /A+|B+/g;
target.match(regExp); // -> ["A", "AA", "B", "BB", "A", "B"]

// 범위를 지정하려면 [] 내에 -를 사용한다. 
regExp = /[A-Z]+/g;
target.match(regExp); // -> ["A", "AA", "B", "BB", "A", "B"]

// 대소문자를 구별하지 않고 알파벳 검색
regExp = /[A-Za-z]+/g;
target.match(regExp); // -> ["A", "AA", "B", "BB", "Aa", "Bb"]

// 숫자를 검색하는 방법 + , 까지 추가
regExp = /[0-9,]+/g;

// \d는 숫자를 의미하고, \D는 문자를 의미한다.
regExp = /[\d,]+/g;
regExp = /[\D,]+/g;

// \w는 알파벳, 숫자, 언더스코어를 의미한다. \W는 반대이다.
regExp = /[\w,]+/g;
regExp = /[\W,]+/g;
```

</aside>

### **📌 31.5.5 NOT 검색**

<aside>
🔅

→ […] 내의 ^은 not의 의미를 갖는다.

- [^0-9]는 숫자를 제외한 문자를 의미한다.

```jsx
const target = 'AA BB 12 Aa Bb';

// 숫자를 제외한 문자열을 전역 검색한다.
const regExp = /[^0-9]+/g;
target.match(regExp); // -> ["AA BB Aa Bb"]
```

</aside>

### **📌 31.5.6 시작 위치로 검색**

<aside>
🔅

→ […] 밖의 ^은 문자열의 시작을 의미한다.

- 단, […] 내의 ^은 not의 의미를 가지므로 주의하기 바란다.

```jsx
const target = 'https://poiemaweb.com';

// 'https'로 시작하는지 검색
const regExp = /^https/;
regExp.test(target); // -> true
```

</aside>

### **📌 31.5.7 마지막 위치로 검색**

<aside>
🔅

→ $은 문자열의 마지막을 의미한다.

```jsx
const target ='https://poiemaweb.com';

// 'com'으로 끝나는지 검사한다.
const regExp = /com$/;
regExp.test(target); // -> true
```

</aside>

### ⭐️31.6 자주 사용하는 정규표현식

### **📌 31.6.1 특정 단어로 시작하는지 검사**

<aside>
🔅

```jsx
const url = 'https://example.com';

// 'http://' 또는 'https://'로 시작하는지 검사한다.
/^https?:\/\//.test(url); // -> true
```

</aside>

### **📌 31.6.2 특정 단어로 끝나는지 검사**

<aside>
🔅

```jsx
const fileName = 'index.html';

// 'html'로 끝나는지 검사한다.
/html$/.test(fileName); // -> true
```

</aside>

### **📌 31.6.3 숫자로만 이루어진 문자열인지 검사**

<aside>
🔅

→ 검색 대상 문자열이 숫자로만 이루어진 문자열인지 검사

```jsx
const target = '12345';

// 숫자로만 이루어진 문자열인지 검사한다.
/^\d+$/.test(target); // -> true
```

</aside>

### **📌 31.6.4 하나 이상의 공백으로 시작하는지 검사**

<aside>
🔅

→ 검색 대상 문자열이 하나 이상의 공백으로 시작하는지 검사한다.

```jsx
const target = ' Hi!';

// 하나 이상의 공백으로 시작하는지 검사한다.
/^[\s]+/.test(target); // -> true
```

</aside>

### **📌 31.6.5 아이디로 사용 가능한지 검사**

<aside>
🔅

→ 검색 대상 문자열이 알파벳 대소문자 또는 숫자로 시작하고 4 ~ 10 자리인지 확인

```jsx
const id = 'abc123';

// 알파벳 대소문자 또는 숫자로 시작하고 끝나며 4 ~ 10 자리인지 검사한다.
/^[A-Za-z0-9]{4,10}$/.test(id); // -> true
```

</aside>

### **📌 31.6.6 메일 주소 형식에 맞는지 검사**

<aside>
🔅

```jsx
export const EMAIL_REGEX =
  /^(?!\.)(?!.*\.\.)[A-Za-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[A-Za-z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:(?!-)[A-Za-z0-9-]{1,63}(?<!-)\.)+(?:[A-Za-z]{2,63}|xn--[A-Za-z0-9-]{2,59})$/;

```

</aside>

### **📌 31.6.7 핸드폰 번호 형식에 맞는지 검사**

<aside>
🔅

→ 검색 대상 문자열이 핸드폰 번호 형식에 맞는지 검사한다.

```jsx
/^\d{3}-\d{3,4}-\d{4}%/.test(cellphone); // -> true
```

</aside>

### **📌 31.6.8 특수 문자 포함 여부 검사**

<aside>
🔅

→ 특수 문자가 포함되어 있는지 검사한다.

```jsx
const target = 'abc#123';
(/[^A-Za-z0-9]/gi).test(target); // -> true
```

</aside>