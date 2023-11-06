## Async/Await (23.07.30)

Callback 함수의 단점을 보완하기 위해 Promise 객체가 탄생했고 Promise 객체의 단점을 보완하기 위해 Async/Await 가 사용된다. 유의해야 할 점이 **async/await가 Promise를 대체하기 위한 기능이 아니라는 것**이다. **내부적으로는 여전히 Promise를 사용해서 비동기를 처리하고, 단지 코드 작성 부분을 프로그래머가 유지보수하게 편하게 보이는 문법만 다르게 해줄 뿐**이라는 것이다.

### 사용법

`**function`** 키워드 앞에 `**async`** 키워드를 붙여주고, 비동기로 처리되는 부분 앞에 `**await`** 키워드를 붙여주면 된다.

```jsx
// 함수 선언식
async function main() {
	const resultData = await getUserData();
}

// 함수 표현식
const main = async () => {
	const resultData = await getUserData();
}
```

async/await의 장점은 비동기적 접근 방식을 동기적으로 작성할 수 있게 해주어 코드가 간결해지며 가독성을 높여져 유지 보수를 용이하게 해준다.

async/await에서 에러가 발생할 경우를 대비해 try-catch 문을 씌워주면 된다.

```jsx
async function func() {
    try {
        const res = await fetch(url);
        const data = await res.json();
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
```

### 주의 사항

1. **async 함수의 리턴 값은 무조건 Promise 객체이다**
    
    ```jsx
    async function main() {
      return 1;
    }
    
    const data = main();
    console.log(data); // fulfilled 상태의 프로미스 객체가 반환된다
    ```
    
    1을 리턴시켜도 무조건 Promise 객체가 반환되는 것을 확인할 수 있다.
    
2. async 함수에도 then 핸들러를 사용할 수 있다.
    
    ```jsx
    async function main() {
      return 1;
    }
    
    main().then(data => console.log(data));
    ```
    
3. await는 Promise 처리가 끝날 때까지 기다린다.
아래 코드에서 `fetch` 요청 → `json` 파싱 → 콘솔 출력 순으로 차례대로 실행된다.
    
    ```jsx
    async function getData() {
      const response = await fetch('https://...');
      const data = await response.json();
      console.log(data):
    }
    ```
    

### 문제 예방 방법

**쓸데없는 await 사용 해결하기**

만약 서로 상관 없는 두 함수를 비동기로 처리하는 상황이 있다고 가정해보자. 이런 경우에는 A 함수와 B 함수 중 어떤 함수가 먼저 처리되어도 상관이 없을 것이다. 그런데 await 를 사용하면 해당 함수 외의 모든 코드의 동작이 중지되기 때문에 A 함수가 위에 있다면 B함수는 쓸데없는 대기 시간이 생기는 것이다. 즉, 상관 없는 두 함수가 쓸데없이 순차적으로 실행된다는 것이다.

```jsx
async function getData(){
  let a = await A(); 
  let b = await B(); 
  console.log(`${a} and ${b}`);
}
```

1. 이런 상황을 해결하기 위해 함수를 변수에 할당해 논블로킹으로 실행한 뒤 나중에 await로 가져오면 되는 것이다.
    
    ```jsx
    async function getFruites(){
    
      let getApplePromise = getApple(); // async함수를 미리 논블록킹으로 실행한다. Promise 객체가 담김
      let getBananaPromise = getBanana(); // async함수를 미리 논블록킹으로 실행한다. 
      
      // 이렇게 하면 각각 백단에서 독립적으로 거의 동시에 실행되게 된다.
      console.log(getApplePromise)
      console.log(getBananaPromise)
      
      let a = await getApplePromise; // 위에서 받은 프로미스객체 결과 변수를 await을 통해 꺼낸다.
      let b = await getBananaPromise; // 위에서 받은 프로미스객체 결과 변수를 await을 통해 꺼낸다.
      
      console.log(`${a} and ${b}`); // 본래라면 1초+1초 를 기다려야 하는데, 위에서 1초기다리는 함수를 바로 연속으로 비동기로 불려왔기 때문에, 대충 1.01초만 기다리면 처리된다.
    })
    ```
    
    그러나 이 방법을 사용하면 비동기 처리 완료 시점을 가늠하기 힘들기 때문에 대부분 `**Promise.all()**` 로 처리한다.
    
2. 다른 방법으로는 `**Promise.all**` 메소드를 사용하는 것이다. 이 방법을 통해 병렬적으로 데이터를 받아올 수 있다.
Promise.all() 은 배열 인자의 각 프로미스 비동기 함수들이 모두 reslove를 반환해야만 결과를 리턴 받는다. 이또한 위 방법처럼 각 프로미스 함수들은 비동기 논블록킹으로 실행되어 시간을 단축 할 수 있다.
    
    ```jsx
    async function getFruites(){
      console.time();
      
      // 구조 분해로 각 프로미스 리턴값들을 변수에 담는다.
      let [ a, b ] = await Promise.all([getApple(), getBanana()]); 
      console.log(`${a} and ${b}`);
      
      console.timeEnd();
    }
    
    getFruites();
    ```
    

내가 이해한 바에 따르면 비동기적 함수를 가져오면 무조건 Promise 객체를 반환하고, 이 Promise 객체에는 상태와 데이터가 담겨있으므로 이를 해석(파싱) 하기 위해 await를 사용하면 내가 원하는 정상적인 데이터로 변경되어 사용이 가능해진다고 보면 될 것 같다.

비동기 함수를 미리 변수에 받아서 논블로킹으로 실행하는 것은 정말 처음 들어본 내용이었다. 이 부분에 대해서는 좀 더 깊은 연구가 필요하다.