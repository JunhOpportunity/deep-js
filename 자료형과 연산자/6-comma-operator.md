## 콤마 연산자 (23.08.02)

> 함수를 간단하게 바꿀 수 있다
> 

```jsx
// 함수 표현식
let a = (obj, value) => {
   obj+=value;
   obj+=value;
   return obj;
}

// 콤마 연산자 사용
let a = (abj, value) => (obj+=value, obj+=value, obj);
```

map() 고차함수나 reduce() 고차함수에도 활용할 수 있다.

```jsx
// 배열에 reduce() 고차함수 사용
let aa = arr.reduce((obj, value) => {
   obj+=value; 
   return obj;
}, 0);

// reduce() 고차함수에 콤마 연산자 활용
let bb = arr.reduce((obj,value) => (obj+=value, obj), 0);
```

주의해야 할 점은 콤마 연산자를 사용하면 코드를 짧게 줄일 수 있지만 가독성에서는 그리 좋지 못한 문법이므로 사용을 지양하는 것이 좋다.
그러나 콤마 연산자를 사용하는 사람이 꽤 있기 때문에 알아두는 것이 좋다.