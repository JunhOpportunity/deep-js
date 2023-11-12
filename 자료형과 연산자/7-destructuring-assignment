# 비구조화 할당 (23.08.04)

> 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담는 표현식
> 

### 배열

```jsx
// 비구조화 할당과 전개 연산자 (...) 사용
var [a1, a2, ...rest_a] = [1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(a1); // 1
console.log(a2); // 2
console.log(rest_a); // [3, 4, 5, 6, 7, 8, 9]
```

**※ 전개 연산자 이후에는 반드시 아무것도 추가해서는 안된다. 전개 연산자가 마지막이 되어야 한다.**

### 객체

```jsx
var { a1, a2, ...rest_a } = { 
	a1 : 10, 
	a2 : 20, 
	a3 : 30, 
	a4 : 40 
};

console.log(a1); // 10
console.log(a2); // 20
console.log(rest_a); // { a3: 30, a4: 40 }
```

`object.key` 형태가 아닌 key 자체를 변수로 만들어서 사용하는 방식
여기서도 전개 연산자가 사용되는데, 나머지 데이터를 객체 형태로 담아둔다.

다른 이름의 변수로도 저장이 가능하다.

```jsx
var { a1 : awesome_name, a2 : dumb , ...rest_a } = { 
	a1 : 10, 
	a2 : 20, 
	a3 : 30, 
	a4 : 40 
};

console.log(awesome_name); // 10
console.log(dumb); // 20
console.log(a1); // Error : a1 is not defined
```

**※** 여기서 변수 선언에 대한 명시가 없을 경우 괄호를 사용해 묶어주어야 한다는 점을 주의하자.

```jsx
({ a, b } = { a : 10, b : 20});
console.log(a); // 10
console.log(b); // 20

{ c, d } = { c : 30, d : 40}; // error
```

### 복사

전개 연산자를 사용하면 깊은 복사가 된다. (새로운 배열로 복사)

```jsx
var arr = [1,2,3];
var copy1 = arr; // 레퍼런스 이어붙이기
var [...copy2] = arr; // 값을 아예 복사
var copy3 = [...arr]; // ''

arr[0] = 'String';
console.log(arr); // [ 'String', 2, 3 ]
console.log(copy1); // [ 'String', 2, 3 ]
console.log(copy2); // [ 1, 2, 3 ]
console.log(copy3); // [ 1, 2, 3 ]
```

객체 역시 전개 연산자를 사용해 깊은 복사가 가능하고, 복사를 하는 동시에 새로운 값도 할당이 가능하다.

```jsx
var prevState = {
  name: "yuddomack",
  birth: "1996-11-01",
  age: 22
};

// 복사하는 동시에 새로운 값을 할당
var state = {
  ...prevState,
  age: 23
};

console.log(state); // { name: 'yuddomack', birth: '1996-11-01', age: 23 }
```

### 활용

> 평소 내가 활용했던 방식
> 

```jsx
// 일반 함수
function renderUser({name, age, addr}){
  console.log(name);
  console.log(age);
  console.log(addr);
}

const users = [
  {name: 'kim', age: 10, addr:'kor'},
  {name: 'joe', age: 20, addr:'usa'},
  {name: 'miko', age: 30, addr:'jp'}
];

renderUser(user);
```

```jsx
// map 함수
const users = [
  {name: 'kim', age: 10, addr:'kor'},
  {name: 'joe', age: 20, addr:'usa'},
  {name: 'miko', age: 30, addr:'jp'}
];

users.map(({name, age, addr}) => {
  console.log(name);
  console.log(age);
  console.log(addr);
});
```

```jsx
// for of 문
const users = [
  {name: 'kim', age: 10, addr:'kor'},
  {name: 'joe', age: 20, addr:'usa'},
  {name: 'miko', age: 30, addr:'jp'}
];

for(var {name : n, age : a} of users){
  console.log(n);
  console.log(a);
}
```