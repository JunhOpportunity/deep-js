### **Spread 연산자 (23.07.25)**

ES6에 새로 추가된 문법으로, 객체 혹은 배열들을 펼칠 수 있게 해주는 연산자
배열이나 객체 앞에 … 을 붙여주면 되는데 **펼쳐진 객체나 배열을 담을 바구니**를 반드시 작성해주어야 한다. (배열, 객체)

**활용**

1. **배열, 객체 합치기**

```jsx
// 배열 합치기
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const arrWrap = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]

// 객체 합치기
const obj1 = {
  a: 'A',
  b: 'B'
};
const obj2 = {
  c: 'C',
  d: 'D'
};
const objWrap = {...obj1, ...obj2};
// {a: 'A', b: 'B', c: 'C', d: 'D'}
```

1. **배열, 객체 복사 (**기존 배열을 보존하기 위한 복사**)**
처음 배열을 펼친 후 배열 안에 다시 넣으면 처음 배열과 똑같이 생겼지만 서로 다른 독립적인 배열이 된다.

```jsx
// 배열 복사
const arr1 = ['a', 'b'];

const arr2 = {...myArray};

console.log(myArray); // ['a', 'b']
console.log(myObject); // ['a', 'b'] // arr1 !== arr2

// 객체 복사
const myObject1 = {
    name: 'JH',
    age: '23'
}

const myObject2 = {...myObject1}; // myObject1 !== myObject2 
```

1. **배열의 나머지 요소 할당**

```jsx
const [first, second, ...rest] = [1, 2, 3, 4, 5];

console.log(first); // 1
console.log(second); // 2
console.log(rest); // [3, 4, 5]
```

1. **문자열 하나씩 쪼개기**
    
    ```jsx
    const stringData = 'abcde';
    const stringArray = [...stringData] // ['a', 'b', 'c', 'd', 'e']
    ```
    
2. **매개변수에 활용**
    - 배열의 값을 인수에 풀어서 전달
        
        ```jsx
        let arr = [3, 5, 1];
        
        alert( Math.max(...arr) );
        alert( Math.max(3, 5, 1) );
        ```
        
    - 나머지 연산자로 파라미터 받기
        
        ```jsx
        function sumAll(...args) {
          let sum = 0;
          for (let arg of args) sum += arg;
          return sum;
        }
        
        alert( sumAll(1) ); // 1
        alert( sumAll(1, 2) ); // 3
        ```
        

**주의사항**

- spread 연산자는 1차원에서만 유효하다.
2차원 배열에 사용하면 1차원 요소만 spread 된다.
```jsx
const arr = [1, 2, 3, [4, 5]]
console.log([...arr]) // [1, 2, 3, [4, 5]]
```