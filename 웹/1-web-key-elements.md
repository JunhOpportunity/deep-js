# 웹 핵심 요소

# Window

> 자바스크립트의 최상위 객체, 전역 객체, 모든 객체가 소속된 객체
> 

Window는 브라우저 창을 의미하며 이 창을 제어할 수 있는 메서드를 제공한다.

## Window의 구성 요소

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c77b689e-2c1c-4a87-8551-170233e3494c/890b95c8-d0a4-4258-8387-2b6bdfe02e42/Untitled.png)

브라우저를 의미하는 window 안에는 다양한 객체들이 트리 형태로 구성되어 있는데, window가 최상위에 위치하고 있다.

DOM, BOM, JS는 사실 Window의 자식이었던 것이다!

## DOM

> 문서 객체 모델, HTML tag들을 브라우저가 이해할 수 있게 객체 형태로 구성한 것
> 

브라우저는 HTML의 tag를 직접 이해할 수 없으므로 우리가 작성한 HTML tag를 이해 가능하게 만들기 위해 DOM tree 형태로 변환해야 한다.

HTML tag는 브라우저가 이해할 수 있는 형태인 JS Node 객체로 변환된다.

### DOM 트리 객체의 구성 요소

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c77b689e-2c1c-4a87-8551-170233e3494c/67ee4e8e-5de9-4c66-93fd-d08b60e50aab/Untitled.png)

- 여기서 TS를 사용할 때 붙여주었던 `HTMLInputElement`가 보인다,

## BOM(Browser Object Model)

> 브라우저 객체 모델, JS가 브라우저와 소통하기 위해 만들어진 모델
> 

JS를 사용해 브라우저의 정보에 접근하거나 브라우저의 여러 기능들을 제어할 수 있는데, 이때 사용하는 객체 모델이 BOM이다.

### BOM 요소

| 이름 | 설명 |
| --- | --- |
| navigator | 브라우저와 버전 정보를 속성으로 가짐 |
| location | 현재 url에 대한 정보, 브라우저에서 사용자가 요청하는 url |
| document | 현재 문서에 대한 정보 |
| screen | 브라우저의 외부 환경에 대한 정보를 제공 |
| history | 현재의 브라우저가 접근했던 url history |

## JavaScript

> DOM, BOM 요소를 조작해 화면을 동적으로 그리는 역할
>