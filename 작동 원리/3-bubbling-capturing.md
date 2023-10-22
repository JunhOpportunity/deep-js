### 버블링 (23.07.09)

> 한 요소에 이벤트가 발생하면 이 요소에 할당된 핸들러가 동작하고, 이어서 부모 요소의 핸들러가 동작하면서 가장 최상단의 조상 요소를 만날 때까지 이 과정이 반복되며 요소 각각에 할당된 핸들러가 동작하는 현상.
⇒ 이벤트가 상위 요소로 전파되는 단계
> 

몇몇 이벤트를 제외하고 거의 모든 이벤트는 버블링 된다.

이벤트가 발생한 가장 안쪽의 요소는 `target` 요소라고 불리고, `event.target` 을 사용해 접근할 수 있다.

`event.target`과 `this`(= `event.currentTarget` )는 다른 것이다.
`event.target`은 실제 이벤트가 시작된 `target` 요소고 버블링이 진행되어도 변하지 않는다.
`this`는 현재 요소로 현재 실행중인 핸들러가 할당된 요소를 말한다.

**버블링 중단하기**
이벤트 버블링은 타깃 이벤트에서 시작해서 `<html>` 요소를 거쳐 `document` 객체를 만날 때까지 각 노드에서 모두 발생한다. 몇몇 이벤트는 `window` 객체까지 거슬러 올라가기도 한다.
이때 버블링을 중단하기 위해 `event.stopPropagation()`을 사용하면 된다.

```jsx
<body onclick="alert(`버블링은 여기까지 도달하지 못합니다.`)">
  <button onclick="event.stopPropagation()">클릭해 주세요.</button>
</body>
```

그런데 여기서 주의할 점은 꼭 필요한 경우를 제외하고 버블링을 막으면 안된다는 것이다.
버블링은 유용하기 때문에 버블링을 꼭 멈춰야 하는 명백한 상황이 아니라면 버블링을 막지 않는 편이 좋다.

`stopPropagation` 으로 버블링을 막아버리면 이벤트 감지를 위한 `document.addEventListener()` 를 사용할 수 없게 되면서 죽은 영역이 되어버린다.

### 캡처링 (23.07.09)

> 이벤트가 하위 요소로 전파되는 단계
> 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e1e7a923-f954-4353-aaca-86a70dbbe247/Untitled.png)

`**<td>**` 를 클릭하면 이벤트가 최상위 조상에서 시작해 아래로 전파되는데 이 단계가 `**캡처링 단계**`이다. 그 후에 이벤트가 타깃 요소에 도착해 실행되는 단계가 `**타깃 단계**`이고 다시 위로 이벤트가 전파되는 단계가 `**버블링 단계**`이다.

addEventListener 핸들러는 타깃 단계와 버블링 단계에서만 실행되는데, true 옵션을 추가해주면 캡처링 단계에서 동작하게 할 수 있다.

```jsx
elem.addEventListener(..., {capture: true})
// 또는
elem.addEventListener(..., true)
```

`capture: false` ⇒ false가 기본값. 버블링 단계에서 동작

`capture: true`  ⇒ 캡처링 단계에서 동작