## 함수를 리턴하는 함수 (23.08.01)

보통 클로저 예제에서 많이 나오는 기법이다.

어떤 경우에 사용하는가?
보통 콜백 함수를 넣는 방법은 이러하다.

```jsx
document.getElementById('c1').addEventListener('click', function(){ console.log(1) });
document.getElementById('c2').addEventListener('click', function(){ console.log(2) });
```

여기서 코드 자체에는 문제가 없으나 같은 코드가 반복된다.
그래서 이런 식으로 바꿔보자.

```jsx
function c(n) {
     console.log(n);
  }

document.getElementById('c1').addEventListener('click', c(n));
document.getElementById('c2').addEventListener('click', c(n));
document.getElementById('c3').addEventListener('click', c(n));
```

그런데 이렇게 되면 이벤트 리스너가 동작하기도 전에 이미 콘솔에 숫자가 출력된다. 함수 자체를 넣어준 것이 아니라 `c()` 함수의 리턴값 자체가 들어가버렸기 때문이다.

그렇다면 어떻게 해야할까?

```jsx
document.getElementById('c1').addEventListener('click', c);
document.getElementById('c2').addEventListener('click', c);
document.getElementById('c3').addEventListener('click', c);
```

그렇다고 이렇게 함수 자체를 넣어버리면 해결은 되지만 모두 같은 동작을 할 것이다.

이럴 때 쓰는 게 바로 함수를 리턴하는 함수이다!

```jsx
// 선언식
function c(n) {
   return function(){
      console.log(n);
   }
}

// 화살표 함수
const c = (n) => () => { // 화살표 함수가 화살표 함수를 리턴
   console.log(n);
}

document.getElementById('c1').addEventListener('click', c(1));
document.getElementById('c2').addEventListener('click', c(2));
document.getElementById('c3').addEventListener('click', c(3));
```

함수 선언식과 화살표 함수 중 마음에 드는 것을 사용하면 된다.
좀 더 직관적으로 함수를 리턴하는 함수라는 것을 보여주기 위해서는 선언식을 사용하면 되고, 좀 더 깜끔한 코드를 자고 싶다면 화살표 함수를 사용하면 된다.