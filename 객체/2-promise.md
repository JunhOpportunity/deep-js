## Promise (23.07.29)

> 비동기 처리란 현재 실행중인 작업과는 별도로 다른 작업을 수행하는 것
> 

보통 비동기 작업이 끝난 뒤 그 결과에 따라 작업을 수행하기 위해 콜백함수를 사용한다.
그러나 콜백함수를 사용하면 코드가 복잡해지고 가독성이 떨어지는 문제가 있다.
또한 여러개의 비동기 작업을 순차적으로 수행해야 할 때는 콜백 함수가 중첩되어 코드의 깊이가 깊어져 콜백 지옥이 만들어 지기도 한다.
이렇게 만들어진 콜백 지옥은 코드의 흐름을 파악하기 힘들어질 뿐 아니라 에러가 발생한 위치를 추적하기조차 힘들다.

이런 콜백함수의 문제를 해결하기 위해 Promise 객체를 사용하는 것이다.

### Promise 객체

```jsx
// 변수로 선언
const varPromise = new Promise((resolve, reject) => {
    const data = fetch('서버로부터 요청할 URL');
    if(data)
    	resolve(data); // 만일 요청이 성공하여 데이터가 있다면
    else
    	reject("Error"); // 만일 요청이 실패하여 데이터가 없다면
})

// 함수로 선언
function funcPromise() {
  return new Promise((resolve, reject) => {
    if {
      resolve();
    } else {
      reject();
    }
  });
}
```

생성된 Promise 객체는 비동기 작업이 완료된 이후 다음 작업을 연결시켜주어야 한다.
`.then()` 과 `.catch()` 를 사용해 성공과 실패에 대한 콜백함수를 등록할 수 있다.

```jsx
myPromise
    .then((value) => { // 성공 후 resolve(data) 호출하게 될 경우 실행
    })
    .catch((error) => { // 실패 후 reject() 호출하게 될 경우 실행
    })
    .finally(() => { // 성공하든 실패하든 무조건 실행
    })
```

위에서 변수로 프로미스 객체를 선언하는 것과 함수로 프로미스 객체를 선언하는 두가지 방법을 사용했는데, 함수로 만드는 것이 좋다.
왜냐하면 재사용할 수 있고, 가독성이 좋고, 확장성도 있기 때문이다.

실무에서는 프로미스 객체를 사용할 일이 있다면 함수로 감싸 사용한다.
또한 자바스크립트에는 비동기 라이브러리 함수도 있는데, 그게 바로 `fetch()`이다.

```jsx
// GET 요청 예시
fetch()
  .then((response) => response.json()) // 응답 객체에서 JSON 데이터를 추출한다.
  .then((data) => console.log(data)); // JSON 데이터를 콘솔에 출력한다.
```

### Promise 3가지 상태

> 진행, 성공, 실패
> 
- Pending(대기 = 진행중) : Promise 객체에 결과값이 채워지지 않은 상태(진행중)
- Fulfilled(이행 = 완료) : Promise 객체에 결과값이 채워진 상태
- Rejected(거부 = 실패) : Promise 객체에 결과값을 채우려고 시도하다가 에러가 난 상태

### Promise 체이닝

> Promise 핸들러를 연달아 연결하는 것
> 

Promise 체이닝을 통해 여러 개의 비동기 작업을 순차적으로 수행할 수 있다.

```jsx
function doSomething() {
  return new Promise((resolve, reject) => {
      resolve(100)
  });
}

doSomething()
    .then((value1) => {
        const data1 = value1 + 50;
        return data1
    })
    .then((value2) => {
        const data2 = value2 + 50;
        return data2
    })
    .then((value3) => {
        const data3 = value3 + 50;
        return data3
    })
    .then((value4) => {
        console.log(value4); // 250 출력
```

체이닝이 가능한 이유는 then 핸들러에서 값을 리턴하면, 그 **반환값은 자동으로 프로미스 객체로 감싸져 반환**되기 때문이다.
다음 then 핸들러에서 반환된 프로미스 객체를 받아 처리하는 것이다.

만약 체이닝 중간에 오류가 있다면 이를 처리하기 위해 catch 핸들러에 점프하도록 설정하면 된다.

```jsx
if () 
	throw new Error('에러입니다')
```

만약 catch 핸들러 다음으로 then 핸들러가 이어서 체이닝 되어 있다면, 에러가 처리되고 가까운 then 핸들러로 제어 흐름이 넘어가 실행이 이어지게 된다.

### Promise 정적 메서드

정적 메서드는 객체를 초기화 & 생성하지 않고도 바로 사용할 수 있기 때문에 비동기 처리를 보다 효율적이고 간편하게 구현할 수 있도록 도와준다.

**Promise.reslove() & Promise.reject()**
프로미스 객체와 전혀 연관없는 함수 내에서 필요에 따라 프로미스 객체를 반환하여 핸들러를 이용할 수 있도록 응용할 수 있다.

```jsx
function getPromiseNumber() {
  const num = getRandomNumber(); // 프로미스 아님
  return Promise.resolve(num); // 프로미스 객체
}
```

**Promise.all()**
배열, Map, Set에 포함된 여러개의 프로미스 요소들을 한꺼번에 비동기 작업을 처리해야 할때 굉장히 유용하다.
**모든 프로미스 비동기 처리가 이행(fulfilled) 될때까지** 기다려서, 모든 프로미스가 완료되면 그때 then 핸들러가 실행하는 형태로 보면 된다. 가장 대표적인 사용 예시로 여러 개의 API 요청을 보내고 모든 응답을 받아야 하는 경우에 사용할 수 있다.

```jsx
// 1. 서버 요청 API 프로미스 객체 생성 (fetch)
const api_1 = fetch("https://jsonplaceholder.typicode.com/users");
const api_2 = fetch("https://jsonplaceholder.typicode.com/users");
const api_3 = fetch("https://jsonplaceholder.typicode.com/users");

// 2. 프로미스 객체들을 묶어 배열로 구성
const promises = [api_1, api_2, api_3];

// 3. Promise.all() 메서드 인자로 프로미스 배열을 넣어, 모든 프로미스가 이행될 때까지 기다리고, 결과값을 출력
Promise.all(promises)
    .then((results) => {
      // results는 이행된 프로미스들의 값들을 담은 배열.
      // results의 순서는 promises의 순서와 일치.
      console.log(results); // [users1, users2, users3]
    })
    .catch((error) => {
      // 어느 하나라도 프로미스가 거부되면 오류를 출력
      console.error(error);
    });
```

**Promise.allSettled()**
`Promise.all()` 메서드의 업그레이드 버전. 주어진 모든 프로미스가 처리되면 모든 프로미스 각각의 상태와 값을 모아놓은 배열을 반환한다.

**Promise.any()**
`Promise.all()` 메서드와 반대 버전. 모든 프로미스 중 **하나라도 완료**되면 바로 반환한다.
만약 모든 프로미스가 거부되면 AggregateError 객체를 반환한다.

**Promise.race()**
`Promise.any()`와 같이 여러 개의 프로미스 중 가장 먼저 처리된 프로미스의 결과값을 반환하지만 하나라도 완료되었을 때가 아니라 하나라도 처리되었을 때 결과를 반환한다. 즉, **실패든 성공이든 하나라도 처리되면 바로 반환**한다는 것이다. 레이싱 경기에서 1등만 기억하는 것이라 생각하면 된다.

### Promise 지옥

콜백 지옥을 해결하기 위해 Promise가 나왔다고 햇는데, Promise 지옥은 또 뭔가 싶을 것이다. 콜백 못지않게 프로미스의 `then()` 메서드가 지나치게 체인되어 반복되면 코드가 장황해지고 가독성이 굉장히 떨어질 수 가 있다.

이를 해결하기 위해 등장한 것이 async/awiat 키워드이다.
then-catch-finally 메서드를 사용하지 않고 비동기 작업을 수행할 수 있다.
async/await 키워드를 사용하면 비동기 작업을 마치 동기 작업처럼 쓸 수 있어서 코드가 간결하고 가독성이 좋아지게 된다.