# Learn Front-end <br/>
<br/>

## 이 문서를 읽기 전에

- 현재 메모를 옮겨오거나 추가하고 있습니다.
- 아직 목차의 순서가 정렬되지 않았습니다, 같은 언어의 개념이라도 순서가 뒤죽박죽 일 수 있습니다.
- 공부하고 있는 개념이기에 정확한 사실에 기반하려 노력했으나, 아닐 수도 있습니다. 다른 자료와 비교해서 봐주세요.
- 하단에 인용하거나 개념을 이해하는데 도움이 되었던 링크를 올리고 있지만 누락되었을 수도 있습니다.
- 온전히 공부하고 이해하기 위한 목적의 문서입니다. 그점 양해 부탁드립니다.

<br/>

## 대목차

- [Javascript](https://github.com/ye-r1/LearnFrontEnd/blob/main/Javascript.md#%EC%9D%B4-%EB%AC%B8%EC%84%9C%EB%A5%BC-%EC%9D%BD%EA%B8%B0-%EC%A0%84%EC%97%90)
- [React](https://github.com/ye-r1/LearnFrontEnd/blob/main/React.md#%EC%9D%B4-%EB%AC%B8%EC%84%9C%EB%A5%BC-%EC%9D%BD%EA%B8%B0-%EC%A0%84%EC%97%90)
- [Typescript](https://github.com/ye-r1/LearnFrontEnd/blob/main/Typescript.md#%EC%9D%B4-%EB%AC%B8%EC%84%9C%EB%A5%BC-%EC%9D%BD%EA%B8%B0-%EC%A0%84%EC%97%90)
- [그 외 자료](https://github.com/ye-r1/LearnFrontEnd/blob/main/README.md#%EC%9D%B4-%EB%AC%B8%EC%84%9C%EB%A5%BC-%EC%9D%BD%EA%B8%B0-%EC%A0%84%EC%97%90)

<br/>

## 소목차

- [1. 브라우저 렌더링의 과정](#1-브라우저-렌더링의-과정)
- [2. 클린코드 작성법](#2-클린코드-작성법)
- [3. Rest API](#3-rest-api)
- [4. CORS (Cross-Origin Resourse Sharing)](#4-cors-cross-origin-resourse-sharing)
- [5. MVC 패턴](#5-mvc-패턴)
- [6. 웹스토리지, 로컬 스토리지, 세션 스토리지, 쿠키](#6-웹스토리지-로컬-스토리지-세션-스토리지-쿠키)
- [7. Eslint](#7-eslint)
- [8. Prettier](#8-prettier)
- [9. Webpack](#9-webpack)
- [](#)
- [](#)
- [](#)
- [](#)
- [](#)

<br/>

## 내용

### 1. 브라우저 렌더링의 과정
1. `Loader` 가 서버로 부터 정보들을 불러온다.<br/>
2. 파싱을 통해 문서를 `DOM` 트리로 만든다.<br/>
3. `DOM` 트리가 구축되는 동안, 브라우저는 `render` 트리를 구축한다.<br/>
4. `CSS` 설정/레이아웃 위치 지정한다.<br/>
5. `rendering` 트리가 그려진다.
 
<br/>

### 2. 클린코드 작성법

1. 어떤 동작을 하는지 처음 보는 사람이 `소스를 다 읽지 않아도 알 수 있게끔` 코드를 작성한다.<br/>
그래서 보통 함수로 별도로 빼서 동사를 사용하여 `어떤 동작`을 하는지 함수 이름으로 설명한다.

```javascript
if(button === "minus") {
  if(count <= 1) return;
}

▽

if(button === "minus" && count > 1)

or

const isAvailbleMinusButton = (button === "minus" && count > 1);
if(isAvailbleMinusButton) {}
```

2. `if문을 중복`으로 사용하는 것 보다 조건을 `한번에` 묶거나 `변수명으로 선언`하여 사용하고,<br/>
- `Boolean`을 나타낼때 isPlus, isMinus처럼 `함수로 분리`해서 쓰는 것이 좋다.


```javascript
if(method === "parse") {
}
```


3. `문자열`로 분기처리 하는 것은 지양해야한다, `side-effect`가 일어날 수도 있기 때문이다.<br/>
`조건 별로 함수로 나누는 것`이 좋다, 왜냐면 side-effect가 생길때 두 조건 `전부 문제`가 생길 수 있기 때문이다.

4. 함수는 `한개의 역할만` 잘 해야한다. 예를 들면 user data를 불러오는 함수는 `불러오는 역할만` 해야한다.<br/>
하지만 해당 함수가 불러오는 것 뿐만 아니라 다른것도 한다면 해당 함수를 `쪼개야`할 수 있다.

```javascript
isMinus(target, id, event, data, isLoading)

▽

isMinus({
  target: "ul",
  id: id,
  event: e.currentTarget,
  data: [{},{},{},{}],
  isLoading: false
})
```

5. 인수는 3개 이하로 사용하는것이 좋다 길면 무슨 역할을 하는지 헷갈릴수 있다.<br/>
대신 함수가 많은 인수를 요구하면 한개의 `config object`로 묶어서 보내는것을 추천한다.

```javascript
data.map((i, idx) => {
})
```

6. 인자값으로 `i` 처럼 이해 못하는 `변수명`을 지양한다.

<br/>

### 3. Rest API
어떤 `URI`(자원)에 어떤 메소드를 사용할지 개발자들 사이에서 널리 쓰이는 약속
- `API`: 지정된 형식으로 요청하면 받을 수 있는 수단.
- `CRUD`: 생성, 읽기, 수정, 삭제를 하는 작업을 통틀어 이르는 말
- `Http 규약`: 서버에 Rest API로 요청을 보낼때 http의 규약에 따라 전송하게 되는것,
`Rest API`에서는 `[Get, Post, Delete, Put, Patch]`를 사용한다.
이중 `[Post, Put, Patch]`에는 `body` 주머니가 있어 몰래 전송이 가능하다.

`Restful` 하게 만든 `API`는 주소만 봐도 파악이 가능하다.
`Post`로 모든 작업을 할 수 있지만 누구든지 요청의 의도를 쉽게 파악할 수 있도록 `Restful` 하게 만들기 위해서는 목적에 따라 구분하여 사용해야 한다.

- `Get`: read
- `Post`: create
- `Put`: 전체 update
- `Patch`: 일부 update
- `Delete`: delete

> `URI`는 동사가 아닌 명사로 이루어져야 한다.
형식이기 때문에 기술에 구애받지 않는다.

<br/>

### 4. CORS (Cross-Origin Resourse Sharing)
도메인 또는 포트가 다른 서버의 자원을 요청하면 발생 하는 문제이다.<br/>
웹 프론트 측에서 `request header`에 `CORS` 관련 옵션을 넣어주고, 서버에서는 해당 프론트 요청을 허용하면 된다.

<br />

### 5. MVC 패턴
시각적인 부분만 수정하려면 `view`에 해당하는 부분만 수정하면 되고<br/>
시각적인 부분과 관계 없이 데이터 처리 부분만 수정하려면 `model` 부분만,<br/>
프로그램간 연결과 제어를 수정하려면 `controller` 부분만 수정하면 되는 방식이다.

- M) `model` - 데이터를 처리하는 역할
- V) `view` - 사용자가 보는 화면
- C) `controller` - 각 요소들을 연결하고 데이터와 시각적 부분의 연결등을 관리한다

> 분리되어있어 유지보수가 편하고 어플리케이션의 확장성과 유연성이 늘어나고 중복코딩의 문제점이 사라진다.<br/>
유저 인터페이스와 비지니스 로직이 분리된다.

<br />

### 6. 웹스토리지, 로컬 스토리지, 세션 스토리지, 쿠키
1. 웹스토리지
- `Key`와 `value` 형태로 이루어진 저장소이다.
- 로컬스토리지와, 세션스토리지가 있다.
- 클라이언트에 대한 정보를 저장한다.
- `HTML5`에서 새로 추가되었다.
- `HTML5`를 지원하지 않으면 사용이 불가능하다.
- `string`만 저장 가능하다.
- 용량이 크다.

1-1) 로컬스토리지
- 영구적으로 데이터를 저장할 수 있다.
- 자동 로그인을 예로 들 수 있다.

1-2) 세션스토리지
- 세션 스토리지는 세션 종료 시 클라이언트에 대한 정보를 삭제한다.
- 에디터 글 자동 불러오기를 예로 들 수 있다.

2. 쿠키
- 대부분의 브라우저가 지원한다.
- 쿠키의 용량이 웹스토리지에 비해 작다.
- 암호화가 없기에 사용자 정보를 도난당할 위험이 있다.
- 로컬에만 정보를 저장합니다.
- ID 자동완성을 예로 들 수 있다.
- 로컬에 저장하기에 공지 메세지를 하루 안보게 하는것도 가능하다.
- 비회원의 장바구니를 예로 들 수 있다.

<br/>

### 7. Eslint
문법적오류나 잠재적 오류까지 찾아내고 오류의 이유를 볼 수 있게 해주는 도구 (ex. `const`의 사용을 `let`으로 제안해주는 것)

<br />

### 8. Prettier
정해진 규칙대로 코드를 예쁘게 변경해주는 도구 (ex. 들여쓰기나 따옴표) 

<br />

### 9. Webpack
`webpack`은 모듈 번들러로 파일 확장자에 맞는 로더에게 위임해 하나로 묶어서 최종 배포용 파일을 만들어준다.<br/>
`<script>` 태그가 여러개 있을 때 순서보장을 맞게 해준다.

<br />

<br/><br/>
> 참조 링크<br/>
https://www.youtube.com/watch?v=Jz8Sx1XYb04<br/>
https://velog.io/@kler/TIL4-%EB%A1%9C%EC%BB%AC%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80-%EC%84%B8%EC%85%98%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80-%EC%BF%A0%ED%82%A4-%EC%A0%95%EB%A6%AC<br/>
https://sunnykim91.tistory.com/121<br/>
