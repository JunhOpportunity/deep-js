### in 연산자 (23.07.24)

**배열 for in 사용** : 인덱스 출력

```jsx
const fruits = ["apple", "banana", "orange"];
for (fruit in fruits) {
    console.log(fruit);
}

// 0 1 2 
```

+) **배열 for of 사용** : 값 출력

```jsx
const fruits = ["apple", "banana", "orange"];
for (fruit of fruits) {
    console.log(fruit);
}

// apple banana orange
```

in 연산자는 객체의 속성을 확인하기 위한 연산자로, 객체가 가지고 있는 프로퍼티 및 메소드의 존재 여부를 Boolean으로 반환하는 역할을 한다.

```jsx
var person = {
  name: "Alice", // name 속성
  sayHello: function() { // sayHello 메서드
    console.log("Alice가 인사합니다.");
  }
};

console.log("name" in person); // true
console.log("sayHello" in person); // true
console.log("age" in person); // false
```

주로 **특정 메소드, 프로퍼티 key값 이름의 존재 여부를 검증하기 위한 목적**으로 많이 사용된다. 즉, 해당 객체에 존재하지도 않는 메소드나 프로퍼티를 동작시킬 경우 에러가 발생할 수 있으므로 사전에 여부를 먼저 확인하기 위한 목적이 크다. ⇒ 최근에 공부했던 예외 처리를 위해 사용한다고 보면 된다.

**활용 방법**

특정 객체에 속성이나 메서드가 없는 경우 새로 추가하게 할 수 있다.

```jsx
if (!("age" in person)) {
  person.age = 25; // age 속성을 추가합니다.
}
```

**in 연산자 특징**

1. **해당 속성이나 메서드의 존재만 확인하고 값은 확인하지 않는다.**
만약 name 속성의 값이 undefined인 경우에도 존재는 true이므로 true 값을 반환한다.
2. hasOwnProperty() 메서드와 비슷하지만 다르다
in 연산자는 상속된 속성이나 메서드도 검사해서 값을 할당하지 않은 상태에서도 존재 여부는 true를 반환하지만
hasOwnProperty() 메서드는 상속된 속성이나 메서드는 아예 없는 것으로 취급한다.

Q. 그렇다면 상속받은 속성이나 메서드를 선언하면 true를 반환하나?