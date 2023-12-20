## Join : 배열 → 문자열

---

> Array.join(기준 문자)
> 

```jsx
const array = ['a', 'b', 'c']
array.join(") // abc
```

## Split : 특정 Separator 통해 자르기

---

> Array.split(분배자)
> 

```jsx
const str = 'The quick brown';

const words = str.split(' ');
console.log(words[1]);

// Expected output: "quick"
```

[String.prototype.split() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split)

### Includes : 특정 문자나 배열 존재 유무 확인 (Boolean)

---

> Array.includes(검색)
> 

```jsx
const str = '1234567';

str.includes(123);
// true
```

### indexOf : 특정 문자나 배열 Index 찾기

---

> Array.indexOf(검색)
> 

**※ 주의 사항 : 존재하지 않는 경우 ‘-1’ 반환**

```jsx
const str = '1234567';

str.indexOf(234);
// 1

str.indexOf(345);
// 2

str.indexOf(111);
// -1
```

### Slice : 원하는 범위를 자르기

String, Array 둘 다 가능

---

> Array.slice(a, b) → a(index) 부터 b(index) 미포함 까지 자르기
Array.slice(a) → a부터 끝까지 자르기
> 

```jsx
const arr = [0, 1, 2, 3, 4, 5];

arr.slice(1); // [1, 2, 3, 4, 5];
arr.slice(1, 3); // [1, 2];
arr.slice(0, -1); // [0, 1, 2, 3, 4]; 마지막 제외하고 자르기
```

### Splice : index부터 n개 자르기

Array만 가능

---

> Array.splice(index, n)
> 

### Reduce : 배열 돌아가면서 연산하기 (초기 숫자 설정)

Array만 가능

---

> Array.reduce((acc, cur) → acc ○ cur, initVal)
> 

```jsx
const str = [1, 2, 3, 4, 5]
let total = 0;

total = str.reduce((acc, cur) -> acc + cur, total)
// 15
```

### ★toString : 10진수 → n진수 변환하기

---

> Number.toString(n진수)
> 

```jsx
let n = 45 // (10진수)
let num = n.toString(3); // (3진수)
```

### ★parseInt : n진수 → 10진수 변환하기

---

> parseInt(n진법 숫자, n진수)
> 

```jsx
let newArray = 1200 // (3진수)
parseInt(newArray, 3); // 45 (10진수)
```

### ★[…string] : 문자열 → 배열 (문자열 자르기)

---

> […String]
> 

```jsx
const string = "12345"
[...string] // ['1', '2', '3', '4', '5']
```

★ **이걸 사용하면 하나씩 자를 경우에 split나 slice나 splice 하지 않아도 된다.** ★

### ★★new Set() : 중복 제거

Object, Array 사용 가능

---

> new Set(Array)
> 

```jsx
let beforeArray = ['1', '1', '2', '3'];

let afterArray = new Set(beforeArray)
// afterArray : {'1', '2', '3'} <- Set 형태

let result = [...afterArray]
// result : ['1', '2', '3'] <- 배열 형태로 변환
```

★ **짧게** 

```jsx
[...new Set(beforeArray)]
```

[Set - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Set)

### Object.values() : 객체의 value 만 뽑아내기

---

> Object.values(객체이름)
> 

```jsx

```

### Object.assign() : 객체들을 중복을 제거해 하나로 묶기 (23.07.21)

---

> Object.assing(객체1, 객체2, …)
> 

```jsx
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };
Object.assign(target, source); // { a: 1, b: 4, c: 5 }
```

### const 로 배열 선언한 경우 배열 재선언 안됨.

push 를 통해 넣어주거나 복사해야함.

```jsx
const array = [];
array = [1, 2, 3] // 불가능.
```

### isNaN (23.10.23)

---

> Number 이 아닌 다른 값 앞에 +를 붙일 경우 NaN 반환하는데, 이때 숫자와 문자를 구분하는 방법
>

```jsx
isNaN('123'); // false
isNaN(12); // false
isNaN(a); // true
```