## 화살표 함수

`**const func = () ⇒ {};**`

### 기본 문법

**매개변수**
화살표 함수의 매개변수가 **하나 뿐**이라면 괄호를 생략할 수 있다.

```jsx
**const func = (name) ⇒ {};
const func = name ⇒ {};**
```

**블록**
함수 블록 내의 코드가 한 줄이고 return 문만 존재한다면 중괄호와 return 키워드를 생략할 수 있다.

```jsx
**const func = name ⇒ { return name };
const func = name ⇒ name;**
```

**객체 리터럴 리턴**
객체 리터럴을 반환하는 경우에 하나의 객체만 반환한다면 위 예시처럼 중괄호와 return 키워드를 삭제할 수 있다. 그러나 반드시 소괄호로 감싸주어야 한다. 왜냐하면 중괄호만 작성하면 함수 블록인지 객체인지 판단할 수 없기 때문이다.

```jsx
**const func = name ⇒ { return { userName: name } };
const func = name ⇒ ({ userName: name });**
```

### **화살표 함수의 중요한 특징**

**화살표 함수에는 this가 없다.**
화살표 함수에서 this 키워드로 접근하면 항상 외부에서 값을 가져온다.
(여기서 외부란 전역 객체 window를 의미한다.)

```jsx
var name = "Global";

let user = {
  name: "local",
  setScope: () => {
    console.log(this.name); 
  }
};

user.setScope(); // Global
```

따라서 이러한 특징 때문에 화살표 함수 내에서 this 키워드를 사용할 때에는 이 점을 명심하고 주의 깊게 사용해야 한다.

**화살표 함수에는 arguments가 없다.**
자바스크립트 함수는 인수에 접근할 수 있도록 유사 배열 객체인 arguments를 지원한다.
하지만 화살표 함수에는 arguments가 없기 때문에 rest parameter 라는 문법을 사용해 인수들을 배열로 받아야 한다.

```jsx
let func = () => {
  console.log(arguments);
}

func(1, 2, 3); // ! Error

let func = (...args) => { // rest parameter
  console.log(args);
}

func(1, 2, 3); // [1, 2, 3]
```

**화살표 함수에는 생성자 함수가 없다**
new 연산자를 사용해 함수를 생성하는 것이 생성자 함수인데, 화살표 함수에는 생성자 함수를 사용할 수 없다.

### 화살표 함수 사용 시 주의사항

**일반 객체의 메소드로 사용하지 말자.**
this 참조를 자주 사용하는 메소드의 경우에 화살표 사용을 피하자.
아까도 말했지만 this 키워드를 사용하면 항상 외부에서 값을 가져오기 때문이다. 

**prototype 메소드로 사용하지 말자.**
화살표 함수 메소드를 prototype 객체로 할당하는 경우에도 일반 객체의 메소드로 사용할 때와 동일한 문제가 발생하므로 이런 경우에는 funciton 키워드를 사용해 일반 함수를 할당하자.

**생성자 함수로 사용하지 말자. (MDJS prototype에 나오는 내용)**
생성자 함수는 prototype 프로퍼티를 가지며 prototype 프로퍼티가 가리키는 프로토타입 객체의 constructor를 사용한다. 하지만 화살표 함수는 prototype 프로퍼티를 가지고 있지 않기 때문에 일반 함수를 사용하자.

**addEventListener의 콜백 함수를 사용할 때도 조심하자.**
콜백 함수로 보통 화살표 함수를 넘겨 사용하는데, 이때 this를 사용하는 경우도 종종 있다. 따라서 이런 경우에는 event 객체의 currentTarget 또는 target 프로퍼티를 사용하여 이벤트가 발생한 요소에 접근하자.

**call & apply & bind 사용으로 this 를 변경할 수 없다.**