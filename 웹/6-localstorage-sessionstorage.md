# 로컬스토리지와 세션스토리지

# LocalStorage & SessionStorage

## LocalStorage

> 로컬에 도메인 별로 지속되는 스토리지
> 
- 시간 제한이 없고 브라우저가 꺼져도 사라지지 않는다
- 값을 지우기 위해 직접 처리해야 한다

## SessionStorage

> 세션(프로세스, 탭, 브라우저)이 종료될 때까지 지속되는 스토리지
> 
- 로컬 스토리지와 쓰임새가 비슷하지만 시간 제한이 있다(설정은 못함)
- 로컬 스토리지는 세션이 종료되면 사라진다

## 쿠키 VS LocalStorage

| 종류 | 쿠키 | 로컬스토리지 |
| --- | --- | --- |
| 접근 | 서버, 클라이언트 양 쪽 | 로컬 환경에서만 |
| 비용 | 모든 쿠키를 다 넘겨야 함 | 개발자가 선별해서 넘기면 됨 |

## 쿠키 VS SessionStorage

| 종류 | 쿠키 | 세션스토리지 |
| --- | --- | --- |
| 만료 기간 | 설정 가능 | 설정 불가능 |
| 데이터 공유 | 같은 브라우저의 경우에 공유 가능 | 공유 불가능 |
| 변화 감지 | 감지 불가능 | 이벤트로 감지 가능 |
| 제한 | 용량, 시간, 갯수 제한 존재 | 용량 제한만 존재 |
| 데이터형 | 문자열만 가능 | JS 객체 저장 가능 |
| 데이터 전송 | 모든 쿠키 전송해야 해서 사이드 이펙트 발생 | 개발자가 선택해서 전송 |
| 이벤트 | 이벤트 없음 | 이벤트 있음 |

## LocalStorage 사용 방법

### 데이터 저장

- 리터럴 방식 : `localStorage.user = “김준호”;`
- 메소드 방식 : `localStorage.setItem(’test’, ‘123’);`

### 데이터 요청

- 리터럴 방식 : `localStorage.user;`
- 메소드 방식 : `localStorage.getItem(’user’);`
- 전체 값 받아오기 : `localStorage.getItem();`

### 데이터 삭제

- 특정 데이터 삭제 : `localStorage.removeItem(’user’);`
- 모든 데이터 삭제 : `localStorage.clear();`

## SessionStorage 사용 방법

> LocalStorage와 똑같다.
>