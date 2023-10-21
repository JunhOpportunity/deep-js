### Event Loop & CallStack (23.07.07)

JS는 Single Thread 이지만 Non Blocking이다. (Single Thread : 한 번에 하나의 작업만 수행)

Memory Heap : 선언한 변수들이 저장되어있는 장소

CallStack : Call 이 Stack 처럼 쌓이는 것(Call은 함수 호출을 의미) 따라서 지금 어느 함수가 실행중인지를 알 수 있다.

Callback Queue : Callback(인자로 전달된 함수)이 Queue 처럼 쌓이는 것. 

```jsx
console.log("1");
setTimeout(function callback() {
	console.log("2");
}, 2000);
console.log("3")

/// 1 -> 3 -> 2
```

**작동 과정**

1. Call Stack에 console.log(”1”) 적재 → 출력 → Call Stack 에서 삭제
2. **Call Stack에 setTimeout 함수 적재 →  Web API 타이머 추가 → Call Stack 에서 삭제**
3. Call Stack에 console.log(”3”) 적재 → 출력 → Call Stack 에서 삭제
4. Web API 타이머 종료 → Callback Queue에 Callback 적재 → Event Loop가 지속적으로 Call Stack 감시 후 Call Stack이 비어있으면 Callback Queue에 적재되어있던 Callback이 Call Stack에 적재 → Callback 실행 → Call Stack에 console.log("2") 적재 → 출력 → Call Stack 에서 삭제 → Callback 삭제

`**동기` `비동기` & `블로킹` `논블로킹`**

`동기` : 코드가 순서대로 실행

`비동기`: 코드가 순서대로 실행 X

`블로킹` : 코드의 실행이 다른 코드의 실행을 막음

`논블로킹` : 코드의 실행이 다른 코드의 실행을 막지 않음.