# 쿠키

## 쿠키란?

> 데이터이면서 현재 사용하는 컴퓨터에 작은 텍스트 파일로 저장되어 있는 것
> 
- 하루 동안 이 창 보지 않기, 일주일 동안 이 창 보지 않기, 로그인 정보 저장, 자동 로그인 등의 기능을 수행할 때 필요한 것이 바로 쿠키이다.
- 브라우저는 내용을 기억할 공간이 없으므로 그것들을 기억하도록 도와주는 것이 쿠키이다.

## 자바스크립트로 쿠키 다루기

`document.cookie` 속성을 사용하여 쿠키를 create, delete, read 할 수 있다

name=value 쌍으로 구성되어있고, 각 쌍은 세미콜론으로 구분한다.

### read

```jsx
document.cookie; // cokie1=value1; cookie2=value2;
```

### write

속성 값으로 path와 만료 기간 설정

```jsx
document.cookie = "user=Junho; path=/; expires=Tue, 19 Jan 2020 00:00:00 GMT"
```

### create

```jsx
document.cookie = "username=김준호";
document.cookie = "username=김준호; expires=Tue, 19 Jan 2020 00:00:00 GMT"
```

### change

초기화 되면서 새로운 값이 저장되는 것이 아니라 추가된다.

### delete

만료 기간을 과거로 바꾸면 삭제된다. 쿠키 요소를 삭제할 때는 반드시 path를 맞춰야 한다.

```jsx
// 1시간 뒤에 쿠키 삭제
document.cookie = "max-age=3600";
```

## 쿠키 파라미터

### name=value

name=value 속성은 데이터를 저장하고 읽는 데 사용하는 속성이므로 쿠키를 사용할 때 반드시 작성해야 한다.

### expires

유효 기간을 설정하는 속성이다.

입력하지 않으면 브라우저가 종료될 때 자동으로 쿠키가 삭제된다.

### max-age

expires의 대안으로, 쿠키 만료 기간을 설정할 수 있다.

쿠키가 생성된 시간을 기준으로 초 단위의 값을 설정할 수 있다.

### Secure

이 속성을 지정하면 해당 쿠키는 SSL을 사용해서만 요청이 가능해진다.

### Domain

도메인 속성을 입력하지 않으면 현재 도메인이 자동 입력된다.

### path

입력하지 않으면 현재 URL이 자동 입력된다.

### httpOnly

httpOnly를 설정하면 자바스크립트에서 쿠키에 접근할 수 없다. 쿠키 조작 방지를 위해 설정하는 것을 권장한다.