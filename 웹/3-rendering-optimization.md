# 렌더링 최적화

# 브라우저 렌더링

브라우저 렌더링은 처음 웹 사이트에 접속했을 때만 실행되는 것이 아니다.

브라우저 렌더링은 특정 조건에 따라 반복적으로 실행된다.

## 렌더링이 반복되는 경우

### 1. 자바스크립트에 의한 노드 추가 혹은 삭제

### 2. 브라우저 창의 리사이징에 의한 뷰포트 크기 변경

### 3. HTML 요소의 레이아웃에 변경을 발생시키는 스타일 변경

이와 같은 경우에는 Layout 계산과 Paint 과정이 다시 실행되면서 리렌더링이 발생하게 된다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c77b689e-2c1c-4a87-8551-170233e3494c/019b44c3-60af-4d0a-9175-b5cab632601f/Untitled.png)

- Reflow : Layout 계산을 다시 수행하는 것
- Repaint : 픽셀을 렌더링하는 Paint 작업을 다시 하는 것

## Reflow

> DOM 요소의 위치와 크기를 다시 계산하는 Layout 과정
> 

Render Tree를 다시 생성하기 때문에 부하가 크고 상위 엘리먼트가 변경되면 하위 엘리먼트에도 영향을 미친다.

노드의 추가와 제거, 위치 변경, 크기 변경, 폰트 변경, 윈도우 리사이징 등의 상황에서 발생한다.

**※ Reflow가 발생하면 Repaint까지 발생하게 되므로 비용이 많이 든다. (Layout 과정 이후에 Paint 과정이 진행되므로 당연하다고 보면 된다.)**

## Repaint

> Layout 과정에는 영향을 미치지 않고 변경된 요소를 화면에 그려줄 때 발생
> 

visibility, backgroundColor, color 등의 변경에 발생한다.

## Reflow VS Repaint

| Reflow | Repaint |
| --- | --- |
| 위치와 크기 변경 시 발생 | 눈으로 보여지는 부분 변경 시 발생 |
| 비용 많음 | 비용 적음 |

## Reflow와 Repaint 최소화 하기

### 1. 영향 받는 노드 최소화하기 (position fixed, absolute)

- 상위 노드의 스타일을 편경하면 하위 노드에 영향을 주기 때문에 다른 엘리먼트 레이아웃에 영향을 주지 않는 fixed와 absolute 속성을 사용하면 비용을 줄일 수 있다.

### 2. 숨겨진 엘리먼트 수정

- display: none 의 경우 Reflow와 Repaint가 발생하지 않는다.
- 많은 수의 엘리먼트를 변경해야 할 때 숨겨진 상태에서 변경하고 다시 보이도록 display: none 속성을 사용하면 Reflow 발생을 최대한 줄일 수 있다.
- 여기서 주의할 점은 visibility: hidden 의 경우에는 보이지 않을 뿐 위치는 차지하기 때문에 Reflow가 발생한다.

### 3. transform, opacity 속성 사용

- 두 속성은 Reflow와 Repaint가 일어나지 않는 속성이다.
- left, right 대신 transform 속성을 사용
- visibility, display 대신 opacity 속성을 사용하면 Reflow와 Repaint 발생을 최소화 할 수 있다.

### 4. 애니메이션 최적화

- 한 프레임의 처리는 16ms(**`60fps`**) 내로 완료되어야 끊기는 현상 없이 자연스럽게 처리
- 자바스크립트에서 setTimeout을 이용하여 애니메이션을 구현한다면 이벤트 루프에 의해 딜레이가 생길 수 있고, 16ms 안에 실행하지 못 한다면 해당 프레임은 유실
- 이를 도와주는 것이 **`requestAnimationFrame()`** 메서드