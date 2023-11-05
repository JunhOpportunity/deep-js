## Call & Apply & Bind

### **Call & Apply**

함수를 호출하는 방법 : 함수 뒤 (), `**call**`, `**apply**`

`**call**` : 평소 사용하던 함수 호출 방식과 동일하게 인자를 넣는다.

`**apply**` : 인자를 하나의 배열로 묶어서 넣는다.

```jsx
var example = function (a, b, c) {
  return a + b + c;
};
example(1, 2, 3);
example.call(null, 1, 2, 3);
example.apply(null, [1, 2, 3]);
```

여기서 특이한 점은 `**call**` 과 `**apply**` 가 공통적으로 인자에 null을 넣었다는 점이다.
null을 인자로 넣은 이유는 this 를 대체하기 위해서다.
this를 대체하기 위해서라고? 이해가 가지 않을 수 있다.
이 코드를 보면 확실하게 이해할 수 있다.

```jsx
// obj 객체에서 this.string의 값은 'zero' 이다.
// 하지만 call 을 사용해 this를 대체하기 위해 새로운 this 값이 들어있는
// obj2 를 null 위치에 넣어준 것이다.
var obj = {
  string: 'zero',
  yell: function() {
    alert(this.string);
  }
};
var obj2 = {
  string: 'what'
};

obj.yell(); // 'zero';
obj.yell.call(obj2); // 'what'
```

obj 객체에서 `this.string`의 값은 `'zero'` 이다.
하지만 `this`를 대체하기 위해  `call` 을 사용해 새로운 `this` 값이 들어있는
obj2 객체를 `null` 위치에 넣어준 것이다.
⇒ 이로써 `zero` 가 아닌 `what` 이 출력 된 것이다! call을 써서 this를 정의해준다면 다른 객체의 파라미터나 메소드를 자기 것처럼 사용할 수 있다.

함수는 arguments 라는 속성을 기본적으로 가지고 있다.
받아온 인자를 배열 형식으로 반환하지만 실제 배열이 아니라 유사 배열이므로 배열의 메소드(map, reduce) 등은 사용이 불가능하다.

```jsx
function example() {
  console.log(arguments);
}
example(1, 'string', true); // [1, 'string', true]
```

이때 call이나 apply 를 사용하면 배열처럼 사용이 가능하다. 배열의 프로토타입에 있는 함수를 빌려 쓰는 것이다.
`**Array.prototype.배열함수.call(arguments)**`

```jsx
function example3() {
  console.log(Array.prototype.join.call(arguments));
}
example3(1, 'string', true); // '1,string,true'
```

### **Bind**

> 함수가 가리키는 this만 바꾸고 호출은 하지 않는 것
⇒ this를 정의하고 함수를 복사해 새로운 함수를 만들어 리턴
> 

```jsx
ar obj = {
  string: 'zero',
  yell: function() {
    alert(this.string);
  }
};
var obj2 = {
  string: 'what'
};

var yell2 = obj.yell.bind(obj2);
```