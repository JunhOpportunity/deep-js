### Getter & Setter (23.07.20)

객체의 프로퍼티를 직접 접근해서 값을 가져오거나 변경하지 말고 Getter & Setter 메서드를 사용하는 것이 좋다. 객체 내부 속성에 직접 접근하지 않아 객체의 **정보 은닉**을 가능하게 해주어 보안을 강화할 수 있고, 코드의 안전성과 **유지보수성**을 높일 수 있기 때문이다. 또한 잘못된 값을 넣을 경우 조건문을 통해 사전에 방지가 가능하다.

ES6 최신 자바스크립트부터는 Getter와 Setter를 get set을 사용해 간단하게 사용이 가능해졌다.

```jsx
const user = {
		name: 'name',
    age: 50,
    get userName() {
    	return user.name;
    },
    set userName(value) {
    	user.name = value;
    }
}

console.log(user.name) // name
console.log(user.userName) // name
```

여기서 주의할 점은 접근자 프로퍼티명과 데이터 프로퍼티명을 중복되게 하면 안된다는 것이다. ⇒ 변수 명과 함수 명을 동일하게 사용하지 마라!

<aside>
❓ **데이터 프로퍼티와 접근자 프로퍼티가 뭐죠?**
- `데이터 프로퍼티` : 객체 내부에 선언된 변수
- `접근자 프로퍼티` : `Getter`와 `Setter` 함수

</aside>
