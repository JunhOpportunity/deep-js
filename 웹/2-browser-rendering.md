# 브라우저 렌더링

# 브라우저 렌더링 과정

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c77b689e-2c1c-4a87-8551-170233e3494c/42a6f1d1-a80f-48d1-9cf3-838b1b87b61f/Untitled.png)

## 1. Parsing

> 파싱을 통해 HTML과 CSS 파일을 브라우저가 이해할 수 있는 트리 구조로 변환
> 

브라우저가 페이지를 렌더링 하려면 가장 먼저 HTML 파일을 해석해야 한다.

HTML 파일은 문자열로 이루어진 텍스트이기 때문에 브라우저가 이해할 수 없으므로 번역이 필요하다.
따라서 브라우저는 파싱을 통해 HTML 파일을 해석하여 DOM Tree를 구성한다.

만약 파싱 중에 HTML에 CSS가 포함되어 있다면 CSSOM(CSS Object Model) Tree 구성 작업도 함께 진행한다.

## 2. Style

DOM Tree와 CSSOM Tree를 결합시켜 렌더링을 위한 Render Tree를 구성한다.

여기서 브라우저에 보이지 않는 것들은 포함되지 않는다.(`visibility: hidden` 속성은 보이지 않지만 공간을 차지하고 있기 때문에 Render Tree에 포함 / `display: none`의 경우에는 공간을 차지하지 않기 때문에 Render Tree에서 제외)

## 3. Evaluate Script

JS 파일을 실행해 동작을 구현한다.

## 4. Layout

Render Tree를 화면에 배치하기 위해 정확한 위치와 크기를 계산한다.

Root부터 노드를 순회하면서 노드의 위치와 크기를 계산하고 Render Tree에 반영한다.

## 5. Paint

Layout 단계에서 계산된 값을 활용하여 노드들을 화면 상의 실제 픽셀로 변환한다.

이때 픽셀로 변환된 결과는 하나의 레이어가 아니라 여러 개의 레이어로 관린된다.

## 6. Composite

Paint 단계에서 생성된 레이어를 합성하여 실제 화면에 나타낸다.

이제서야 웹 페이지가 나타난다.