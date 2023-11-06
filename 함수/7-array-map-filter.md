## map() VS filter() (23.07.31)

> 차이점 : 리턴하는 기능이 다르다
> 

`**map**` : 새로운 배열 요소를 생성해 반환한다.

`**filter**` : true를 반환하면 요소를 유지하고, false를 반환하면 요소를 버린다.

```jsx
var testArray = [0,1,2,3,4,5];

testArray.filter(function(c){ return c * 2; });
// [1, 2, 3, 4, 5] <- filter 함수는 true를 반환하면
// 그냥 요소를 유지한 채 반환한다. 즉, 산술이 아닌 논리로본다.
// 0을 제외한 모든 값은 true 이므로 0을 제외한 모든 요소를
// 그대로 반환하는 것이다.

testArray.map(function(c){ return c * 2 });
// [0, 2, 4, 6, 8, 10]
```

좀 애매한 예시라면 이 예시로 확실해진다.

```jsx
var testArray = [0,1,2,3,4,5];

testArray.filter(function(c){ return c <= 2; }); 
// [0, 1, 2]
// filter은 참과 거짓만을 판단해 참 요소만을 그대로 반환한다.

testArray.map(function(c){ return c <= 2 }); 
// [true, true, true, false, false, false]
// map은 결과를 반환한다.
```
