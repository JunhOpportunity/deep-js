## Reduce 고차함수 (23.07.31)

**`array.reduce( (acc, cur, index, arr) ⇒ () , initialValue )`**

- `acc` : 누적 반환 값 (더하기를 계속 했으면 더해진 값, 곱하기를 계속 했으면 곱해진 값)
- `cur` : 현재 값
- `index` : 인덱스 값
- `arr` : 현재 배열 전체
- `initialValue` : 시작 값 (없을 경우 배열 첫 번째 값. 빈 배열일 경우 에러 발생), 배열이나 객체를 넣어서 원하는 타입으로 반환하게 하는 방법도 있다.

```jsx
const numbers = [1, 2, 3, 4];

const sumByPlus = numbers.reduce((number1, number2) => number1 + number2);
const sumByMinus = numbers.reduce((number1, number2) => number1 - number2);
const sumByMulti = numbers.reduce((number1, number2) => number1 * number2);

console.log(sumByPlus); // 10
console.log(sumByMinus); // -8
console.log(sumByMulti); // 24
```

참고로 `reduceRight` 고차함수를 사용하면 배열을 거꾸로 수행한다.

### 활용

- 객체 배열 계산
    
    ```jsx
    var initialValue = 0;
    var list = [
        { x : 1 },
        { x : 2 },
        { x : 3 }
    ];
    var sum = list.reduce(function (acc, cur) {
        return acc + cur.x;
    }, initialValue)
    
    console.log(sum)
    ```
    
- 2차원 배열 펼치기
    
    ```jsx
    var arr = [
        [0, 1],
        [2, 3],
        [4, 5]
    ]
    var flattened = arr.reduce(function(acc, cur) {
            return acc.concat(cur);
        }
    ,[]);
    
    // 또는
    var flattened = arr.reduce(function(acc, cur) {
         return acc = [...acc, ...cur];
        }
    ,[]);
    
    console.log(flattened); //[0, 1, 2, 3, 4, 5]
    ```
    