### 예외(Exception) &  예외 처리(Exception Handling) (23.07.23)

> 예외란 실행 중인 프로그램에서 예기치 못한 상황이 발생하여 더이상 진행할 수 없는 상황을 말한다
> 

예외 상황은 프로그램의 실행을 중단시키거나, 비정상적인 결과를 초래할 수 있으므로, 프로그래머는 이러한 예외를 발생하지 않도록 미리 방지하는 것도 중요하지만, 발생한 예외를 처리할 수 있는 방법을 마련해야 한다.

이를 위해 `try-catch` 문을 사용할 수 있다.

**try - catch - finally**

- try
예외가 발생할 가능성이 있는 코드를 입력하는 부분
- catch
try 부분에서 예외가 발생했을 때 처리하는 부분
- finally
에러 발생 여부와 상관 없이 반드시 실행되어야 하는 코드를 입력하는 부분
`break` `return` 등 try-catch 문을 빠져나가려는 어떠한 경우에도 반드시 실행됨

**예외 직접 발생**

`throw`를 사용해 예외 객체를 직접 만들어서 발생시킬 수 있다.

```jsx
try {
	console.log("코드 실행!")
	throw new Error("예외 발생시키기")
} catch (error) {
	console.log("Exceptrion 발생!")
}
```

이는 개발자가 예외를 던져서 예외 상황을 감지하고, 이를 적절하게 처리할 수 있도록 할 수 있다.

🚩**사용자  정의 에러** 
자바스크립트에서 커스텀 예외를 만들려면 ~~Error~~ 클래스를 상속받아 새로운 클래스를 만들어야 한다.

```jsx
class MyError extends Error {
  constructor(message) {
    super(message);
    this.name = 'MyError';
  }
}
```

**다중 예외 처리**

1. `**instanceof` 연산자를 사용하여 처리**

```jsx
try {
  // ...
} catch (error) {
  if (error instanceof TypeError) {
    console.error("TypeError: " + error.message);
  } else if (error instanceof ReferenceError) {
    console.error("ReferenceError: " + error.message);
  } else if (error instanceof SyntaxError) {
    console.error("SyntaxError: " + error.message);
  } else if (error instanceof RangeError) {
    console.error("RangeError: " + error.message);
  } else {
    console.error("unexpected error: " + error);
  }
}
```

1. `**error.name` 프로퍼티를 사용하여 처리**

```jsx
try {
  // 에러가 발생할 수 있는 코드
} catch (error) {
  if (error.name === "ReferenceError") {
    // 참조 에러
  } else if (error.name === "SyntaxError") {
    // 구문 에러
  } else if (error.name === "TypeError") {
    // 타입 에러
  } else {
    // 예외
  }
}
```

**Stack**
함수를 여러개 호출하는 함수에서 에러가 발생했거나 여러 함수가 얽혀있는 함수에서 에러가 발생한 경우 Stack을 사용해 추적할 수 있다.

**완료되지 않은 함수는 Call Stack 에 쌓인다. 자바스크립트 인터프리터는 함수의 호출 과정을 모두 추적하고 있기 때문에, 발생한 에러는 Call Stack 어디에서든 캐치할 수 있다.**

**비동기 함수 예외 처리**

**try-catch 문은 기본적으로 동기적으로 동작**한다. 그래서 setTimout 같은 비동기 코드에서 발생한 예외는 잡아낼 수 없다. (setTimeout에 넘겨진 함수는 try-catch를 떠난 다음에야 실행되기 때문이다.)
따라서 try-catch 문을 사용해 비동기 함수에서 예외 처리를 해야 한다면 setTimeout 함수 내부에 에러 처리 함수를 구현해주어야 한다.

```jsx
setTimeout(function() {
  try {
		// 예외가 발생할 것 같은 코드 작성
  } catch {
    console.log("비동기 함수 예외 처리 성공!")
  }
}, 1000);
```