# Learn Front-end <br/>
<br/>

## 이 문서를 읽기 전에

- 현재 메모를 옮겨오거나 추가하고 있습니다.
- 아직 목차의 순서가 정렬되지 않았습니다, 같은 언어의 개념이라도 순서가 뒤죽박죽 일 수 있습니다.
- 공부하고 있는 개념이기에 정확한 사실에 기반하려 노력했으나, 아닐 수도 있습니다. 다른 자료와 비교해서 봐주세요.
- 하단에 인용하거나 개념을 이해하는데 도움이 되었던 링크를 올리고 있지만 누락되었을 수도 있습니다.
- 온전히 공부하고 이해하기 위한 목적의 문서입니다. 그점 양해 부탁드립니다.

<br/>

## 목차
- [1. this](#1-this)
- [2. call, apply, bind](#2-call-apply-bind)
- [3. arrow function](#3-arrow-function)
- [3-1. arrow function을 사용해서는 안되는 경우](#3-1-arrow-function을-사용해서는-안되는-경우)
- [4. data type](#4-data-type)
- [5. let, const, var의 차이점](#5-let-const-var의-차이점)
- [6. hoisting](#6-hoisting)
- [7. curring 함수](#7-curring-함수)
- [8. HOF (High Order Function) 고차함수](#8-hof-high-order-function-고차함수)
- [9. Eslint](#9-eslint)
- [10. Prettier](#10-prettier)
- [11. Webpack](#11-webpack)
- [12. CORS (Cross-Origin Resourse Sharing)](#12-cors-cross-origin-resourse-sharing)
- [13. Rest API](#13-rest-api)
- [14. JSX](#14-jsx)
- [15. FLUX](#15-flux)
- [16. 서버사이드렌더링, 클라이언트사이드렌더링](#36-서버사이드렌더링-클라이언트사이드렌더링)
- [17. SPA (single page application)](#37-spa-single-page-application)
- [18. 리액트 성능개선 방법](#17-리액트-성능개선-방법)
- [19. null, undefined](#18-null-undefined)
- [20. ajax, fetch, axios](#19-ajax-fetch-axios)
- [21. promise, async await](#20-promise-async-await)
- [22. 프레임워크, 라이브러리](#21-프레임워크-라이브러리)
- [23. 함수형 컴포넌트, 클래스형 컴포넌트](#22-함수형-컴포넌트-클래스형-컴포넌트)
- [24. React](#23-react)
- [25. useCallback / useMemo](#24-usecallback--usememo)
- [26. custom hook의 use case, 장점](#25-custom-hook의-use-case-장점)
- [27. 웹스토리지, 로컬 스토리지, 세션 스토리지, 쿠키](#26-웹스토리지-로컬-스토리지-세션-스토리지-쿠키)
- [28. Script async, defer](#29-script-async-defer)
- [29. "use strict"](#30-use-strict)
- [30. number](#31-number)
- [31. rest 파라미터와 spread 연산자](#32-rest-파라미터와-spread-연산자)
- [32. Node.js](#33-nodejs)
- [33. 브라우저 렌더링의 과정](#34-브라우저-렌더링의-과정)
- [34. MVC 패턴](#35-mvc-패턴)
- [35. event bubbling](#38-event-bubbling)
- [36. event loop](#39-event-loop)
- [37. 함수형 프로그래밍](#40-함수형-프로그래밍)
- [](#)
- [](#)
- [](#)
- [](#)
- [](#)

<br/>

## 내용

### 1. this
자바스크립트의 `this`는 호출하는 방법에 의해 결정이 된다.<br/>
누가 불렀는지에 따라서 `this`의 의미가 달라진다.

``` javascript
var people = {
  name: "ye-r1",
  whoAmI: function (){
    console.log(this);
  }
}

people.whoAmI();  //people

var newPeople = people.whoAmI;
newPeople();  //window

var bindNewPeople = newPeople.bind(people); //people

btn.addEventListener("click", people.whoAmI); //btn

```

객체를 생성할때 사용하는 생성자함수는

``` javascript
function Person(name, job){
    this.name = name;
    this.job = job;
}

Person("ye-r1", "free");

window.name => "ye-r1"
window.job => "free"
```

그냥 사용하게되면 `window`에 저장하라는 뜻과 같다.

``` javascript
new Person("ye-r1", "free");

Person.name => "ye-r1"
Person.job => "free"
```

`new`를 붙여주어야 생성자 본인을 `this`로 가리키게 된다.

화살표 함수에서의 `this`는 언제나 상위 스코프의 `this`를 가리킨다. 이를 `Lexical this`라고 한다.

> 또한 화살표 함수는 `call, apply, bind` 메소드를 사용하여 `this`를 변경할 수 없다.<br/>
"use strict" 모드에서는 `window` 객체를 `this`를 통해 참조할 수 없기 때문에 `undefined`가 나올 수 있다.

<br />

### 2. call, apply, bind

이는 함수에 `this`를 바인딩 하기 위한 방법이다.
- `call`은 `this`를 바인딩 하면서 두번째 인자를 `,` 쉼표로 이어서 호출한다.
- `apply`는 `call`과 동일하지만 두번째 인자를 `[a,b,c,d]` 배열로 호출한다.
- `bind`는 함수를 호출하는 것이 아닌 `this`가 바인딩 된 새로운 함수를 리턴한다.

<br/>

### 3. arrow function
화살표 함수는 `Lexical this`를 지원하므로 콜백 함수로 사용하기 편리하다. 

<br/>

### 3-1. arrow function을 사용해서는 안되는 경우

1. 메소드

``` javascript
const people = {
  name: "ye-r1",
  whoAmI: () => {
    console.log(this.name);
  }
};

people.whoAmI(); // undefined
```

메소드에 화살표 함수를 쓸 경우에는 `window` 전역을 가르키는데 그것이 "use strict" 모드에서는 `undefined`가 뜬다.

> 메소드에 화살표함수로 작성하고 싶을때에는 축약 메소드의 표현을 활용한다.

``` javascript
const people = {
  name: "ye-r1",
  whoAmI() {
    console.log(this.name);
  }
};

people.whoAmI(); // "ye-r1"
```

2. 프로토타입

화살표 함수로 정의된 메소드를 `prototype`에 할당하는 경우에도 동일한 문제가 발생한다.

``` javascript
const people = {
  name: "ye-r1"
};

Object.prototype.whoAmI = function() {
  console.log(this.name);
};

people.whoAmI(); // "ye-r1"
```

3. 생성자 함수
화살표 함수는 생성자 함수로 사용할 수 없다.<br/>
생성자 함수는 `prototype` 프로퍼티를 가지며 `prototype` 프로퍼티가 가리키는 프로토타입 객체의 `constructor`를 사용한다.<br/>
하지만 화살표 함수는 `prototype` 프로퍼티를 가지고 있지 않다.<br/>
<br/>
4. addEventListener의 콜백함수<br/>
`addEventListener` 함수의 콜백함수를 화살표 함수로 정의하면 `this`가 상위 컨텍스트인 전역 객체 `window`를 가리킨다.<br/>
따라서 일반 함수를 사용하여야 한다.

<br/>

### 4. data type
자바스크립트의 데이터 타입에는 크게 두가지로 나눌 수 있다.

1. 원시형

  `string, number, boolean, null, undefined`
  
  - 원시형은 데이터의 값 그 자체를 의미한다.
  - 용량이 작아 자체를 저장하며, 데이터의 값이 변경될 때에는 주소 자체를 변경시킨다.
  - 이로 인해서 자바스크립트의 원시형은 불변성을 띄는 데이터 타입이다.
  
2. 참조형

  `function, array, object`
  
  - 참조형은 용량이 커 데이터가 담긴 주소를 저장하며, 가변값이다.

<br />
  
### 5. let, const, var의 차이점

- `let`과 `const`는 es5 이후에 나온 신문법이다.<br />
기존 변수와 상수를 구분하지 않고 사용하던 `var`를 대신하기 위해 나왔다.<br/>
- `let`, `const`과 `var`는 스코프가 다르다.<br/>
`let`, `const`는 실행 컨텍스트가 블럭 스코프를 지원하며 `{}` var는 함수스코프를 지원한다. `function {}`<br/>
- `var`는 호이스팅으로 올라가 선언하기 전에도 값을 찍을 수 있다.<br/> 값이 할당되지 않았기 때문에 `undefined`가 뜬다.<br/>
반면 `let`과 `const`는 호이스팅을 지원하지만 막아두어서 에러가 발생한다.

### 6. hoisting
데이터를 선언하기 전에 호출했을때 아래에 있는 선언부분이 최상단으로 올라가지는 현상이다.<br/>
함수 선언은 함수 몸체가 `hoisting` 되는 반면에, 변수 선언 상태로 작성된 함수는 변수 선언만 `hoisting` 된다.

### 7. curring 함수
커링 함수의 인자로 함수를 전달하면 기능이 추가된 새 함수로 반환할 수 있다.<br/>
객체형 프로그래밍의 `extend` 상속기능 처럼 함수형 언어에서도 사용할 수 있도록 도와주는 함수이다.

``` javascript
//기존방법
function multiply(a, b) {
  return a * b;
}

function multiplyTwo(a) {
  return multiply(2, a);
}

multiplyTwo(4);
```

``` javascript
//커링함수
function multiply(a, b) {
  return a * b;
}
function multiplyX(x) {
  return function(a) {
    return multiply(a, x);
  }
}

multiplyX(2)(3);

or

const multiplyTwo = multiplyX(2);
multiplyTwo(3);

```

`const formula = x => addFour(multiplyThree(multiplyTwo(x)));`<br/>
이렇게 사용하게 되면 우리가 생각하는 실행방향은 -> 지만<br/>
사실상 함수가 실행하는 순서는 <- 거꾸로 실행되는 것이 헷갈릴 수 있다.<br/>
<br/>
이 함수의 실행 순서를 -> 처럼 바꾸기 위해서는 `reduce` 함수를 사용할 수 있다.

``` javascript
const formula = [
  multiplyTwo,
  multiplyThree,
  addFour
].reduce(function(prev, next) {
  return function(x) {
    return next(prev(x));
  }
}, k => k);

```

이것을 더 간결하게 사용하면 이렇게 작성하면 된다.


``` javascript
function compose(...arg) {
  return args.reduce(function(prev, next) {
    return function(...values) {
      return next(prev(...values));
    }
  }, k => k);
}

const formula = compose(
  multiplyX(2),
  multiplyX(3),
  multiplyX(4)
);
```

### 8. HOF (High Order Function) 고차함수

``` javascript
const formula = compose(
  multiplyX(2),
  multiplyX(3),
  multiplyX(4)
);
```

위에 있는 이 `compose`가 고차함수이다.<br/>
함수를 받아 함수를 반환한다.


<br />

### 9. Eslint
문법적오류나 잠재적 오류까지 찾아내고 오류의 이유를 볼 수 있게 해주는 도구 (ex. `const`의 사용을 `let`으로 제안해주는 것)

<br />

### 10. Prettier
정해진 규칙대로 코드를 예쁘게 변경해주는 도구 (ex. 들여쓰기나 따옴표) 

<br />

### 11. Webpack
`webpack`은 모듈 번들러로 파일 확장자에 맞는 로더에게 위임해 하나로 묶어서 최종 배포용 파일을 만들어준다.<br/>
`<script>` 태그가 여러개 있을 때 순서보장을 맞게 해준다.

<br />

### 12. CORS (Cross-Origin Resourse Sharing)
도메인 또는 포트가 다른 서버의 자원을 요청하면 발생 하는 문제이다.<br/>
웹 프론트 측에서 `request header`에 `CORS` 관련 옵션을 넣어주고, 서버에서는 해당 프론트 요청을 허용하면 된다.

### 13. Rest API
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

### 14. JSX
- `JS XML` 약자
- 자바스크립트 확장 문법
- 자바스크립트와 xml을 혼합해서 사용하는 방식
- `react.createElement( )`을 생성하여 편하게 `html`으로도 작성 가능하게 한다.
`cra`를 하게 되면 `webpack`에서 바벨로 처리해준다.

<br/>

### 15. FLUX
- MVC 패턴의 문제점을 개선한 패턴이다.
- MVC 패턴으로 진행하게되면 규모가 커지면서 Model 관리가 어려워진다.
- 단방향 데이터 흐름을 띄는 아키텍쳐이다. (→ 추적이 쉽다, 관리하기 쉽다)
- UI 데이터만 전달받는다.
- UI 데이터 변경시 직접 `store`와 동기적으로 연결하지 않고, `action`을 일으켜 변경사항을 업데이트한다.


<br/>

### 16. 서버사이드렌더링, 클라이언트사이드렌더링
**서버사이드 렌더링 (SSR)** <br />
> 서버사이드 렌더링`(SSR)` 은 페이지를 이동할 때마다 새로운 페이지를 요청한다.<br />
서버 연산을 통해서 렌더링하고 완성된 페이지 형태로 응답한다.
  
장점<br />
- 페이지를 이동할때마다 서버에 요청한다. => 서버에서 렌더링
- 소스를 전부 불러오기 때문에 검색엔진`(SEO)` 최적화에 좋다.
- 첫 렌더링된 `html` 을 클라이언트에게 전달해 주기때문에 초기 로딩 속도를 많이 줄여 줄 수 있다.
- 자바스크립트 파일을 불러오고 렌더링 작업이 완료되기 전에 사용자가 사이트 컨텐츠를 이용할 수 있게된다.

단점<br />
- 페이지 이동시 깜빡임이 있다.
- 중복리소스와 자원낭비가 심하다.
- 프로젝트가 커지면 복잡할 수 있다.

**클라이언트 사이드 렌더링(CSR)** <br />
> 클라이언트에서 렌더링하는 방식이다. `(Client Side Rendering)`

장점<br />
- 첫 요청할때 한페이지만 불러오게 된다. →  `React` 를 보면 `index.js` 만 불러오게 된다.(Single Page Application)
- 필요한 데이터만 서버에 요청하기 때문에 비교적 트래픽 감소가 있다. => 클라이언트에서 렌더링
- 깜빡이지 않기에 사용자 경험이 올라간다. (`native app`과 동일한 사용경험을 준다.)
- 그 후, 사용자의 행동에 따른 필요한 부분만 다시 읽어들이기 때문에 서버 측에서 렌더링하여 전체 페이지를 다시 읽어들이는 것보다 빠른 인터렉션을 기대할 수 있다.
- 페이지 이동시 렌더링이 빠르고, 코드 재사용성이 높다.

단점<br />
- 검색엔진을 최적화 하려면 따로 `SSR` 렌더링이 필요하다.
- `SPA`방식이라 한번에 필요한 데이터를 전부 가져와 초기 속도가 오래 걸린다.

<br />

### 17. SPA (single page application)
`SPA`는 기본적으로 웹 애플리케이션에 필요한 모든 정적 리소스를 최초에 한번 다운로드한다.<br/>
이후 새로운 페이지 요청 시, 페이지 갱신에 필요한 데이터만을 전달받아 페이지를 갱신하므로 전체적인 트래픽을 감소할 수 있고<br/>
전체 페이지를 다시 렌더링하지 않고 변경되는 부분만을 갱신하므로 새로고침이 발생하지 않아 네이티브 앱과 유사한 사용자 경험을 제공할 수 있다.<br/>
<br/>
모바일의 사용이 증가하고 있는 현 시점에 트래픽의 감소와 속도, 사용성, 반응성의 향상은 매우 중요한 이슈이다.<br/>
`SPA`의 핵심 가치는 사용자 경험(UX) 향상에 있다.

<br />

### 18. 리액트 성능개선 방법

- 첫 페이지 로딩 지연문제를 해결한다. => 첫 페이지의 `SSR` (Server Side Rendering)
- 컴포넌트 `lazy loading`을 추가한다.
- 이미지 `lazy loading`을 추가한다.
- 네트워크 탭의 성능을 추적한다.
- `Re-rendering`을 최소화시킨다.
- 중복계산을 줄인다 (`UseEffect`, `UseMemo`)
- 스켈레톤을 추가한다. (ui-ux 관점)

<br/>

### 19. null, undefined
- 값이 없는 것을 뜻한다.
- `var`, `let`과 같이 데이터에 값이 할당되지 않았을때 `undefined`가 기본으로 할당된다.
- 하지만 `null`은 의도적으로 값이 비어있음을 표현한 것이다.

<br/>

### 20. ajax, fetch, axios
ajax<br/>
`HTML` 페이지 전체가 아닌 일부분만 갱신할 수 있도록 `XMLHTMLRequest` 객체를 서버로부터 요청하는 자바스크립트 비동기 통신방식이다.<br/>
구현의 불편함을 느낀 사용자들이 `jQuery`를 통해 구현하기 시작했고, 그 이후 `es6`의 표준인 `fetch API`가 표준으로 나오게 되었다.

- `fetch`: `ie`를 제외한 대부분의 브라우저에서 `IMPORT`없는 `Web API`를 사용 가능, 반환값으로 `promise`를 가진다.
- `axios`: `node.js`와 브라우저를 위한 비동기통신 라이브러리, `fetch`와 달리 ie11도 지원, 반환값으로 `promise`를 가진다.

**ajax의 단점** <br/>
단점<br/>

- 브라우저에서 JavaScript가 비활성화된 경우 작동하지 않는다.
- 일부 웹 크롤러는 JavaScript를 실행하지 않으며 JavaScript에 의해 로드된 콘텐츠를 볼 수 없다.
- SPA의 대부분의 단점과 같다.

<br/>

### 21. promise, async await
`promise`는 비동기 동작 다루기 위한 오브젝트이다.
- 콜백지옥을 막아줄 수 있고, 비동기 데이터를 가지고 성공 - 실패를 제어할 수 있다.

`async await`
- 자바와 같이 동기적 코드 흐름으로 개발이 가능하다.
- 코드가 간결해지고, 가독성이 높아진다.
- try / catch로 에러를 핸들링할 수 있다.
- error가 어디서 발생했는지 알기 쉽다.

<br/>

### 22. 프레임워크, 라이브러리
프레임 워크: 어플리케이션 개발을 위한 뼈대, 개발이 빨라진다.<br/>
라이브러리: 어플리케이션의 기능을 빠르게 구현 제공하는 기능, 기능이라 개발 자유도가 높다
<br/>

### 23. 함수형 컴포넌트, 클래스형 컴포넌트
함수형 컴포넌트<br/>
- 짧은 코드로 구현가능한 신문법이다.
- 클래스 컴포넌트 보다 메모리 자원을 덜 사용한다.
- 빌드 후 배포시에 결과물의 크기가 작다.
- `hook` 지원으로 `state` 관리가 쉽다.
- 함수형 컴포넌트는 렌더링된 값들을 고정시킨다.

클래스형 컴포넌트<br/>
- 라이프 사이클 `API`의 사용이 가능하다.
- `render` 함수가 반드시 존재해야 한다.
- `render` 함수가 반드시 존재해야 한다.
<br/>

### 24. React
`spa`로 이루어진 프론트앤드 자바스크립트 라이브러리

<br/>

### 25. useCallback / useMemo
`useMemo` 는 특정 결과값을 재사용 할 때사용하고<br/>
`useCallback` 은 특정 함수를 재사용하고 싶을때 사용한다.<br/>
계속 바뀌는 값에 대해서는 `useMemo`로 최적화를 시켜주고 `deps`를 지정해주어야한다.<br/>
= props로 전달받은 함수는, props나 상태가 업데이트될 때마다 새로 생성이 된다.<br/>
재계산 하는 함수가 아주 간단하다면 성능상의 차이는 미미하겠지만 더 안좋을 수도 있다.<br/>
만약 재계산 하는 로직이 복잡하다면 `useMemo`를 사용함으로써 불필요한 렌더링을 막을 수 있다.

<br/>

### 26. custom hook의 use case, 장점
반복되는 로직을 쉽게 재사용하기 위해 사용하였고, side-effect (부작용)을 방지할 수 있다.

<br/>

### 27. 웹스토리지, 로컬 스토리지, 세션 스토리지, 쿠키
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

### 28. Script async, defer
`<script async>`
- 파싱중에 동시에 다운받고 다운이 끝나면 파싱을 잠시 중단하고 실행한다.
- 파싱중 실행구문을 실행시킨것이기에 조작하려는 시점에 `html`들이 없어 위험할 수 있다.
- 실행구문을 불러오는 중에는 `html` 파싱이 중단되므로 페이지 로딩이 오래걸린다.
- script 코드가 순서의 의존적인거라면 `async` 옵션은 로딩에 문제가 걸릴 수 있다.

`<script defer>`
- 파싱중에 동시에 다운받고 기다리다가 `html`파싱이 완료되면 실행한다.
- 파싱하는 동안 다운받고 `html` 파싱이 완료된 후에 실행이 되기 때문에 좋다.

<br/>

### 29. "use strict"
자바스크립트 엄격모드<br/>
비 상식적인 구문을 에러시킨다.<br/>
"보안" 자바스크립트를 작성하는 쉬운 방법이다.

<br/>

### 30. number
- 자바스크립트는 `number` 종류가 하나만 있다.
- 다른 언어에서는 용량, 속성에 따라 다르게 선언해야한다.
- 하지만 자바스크립트에서는 굳이 `number`라고 선언하지 않아도 다이나믹하게 자기가 결정한다.
- 자바스크립트에서는 정수나 소수점 상관없이 `number`라고 알아서 정의가 된다.
- 숫자를 `0`으로 나누면 `infinity`로 나오고 음수의 숫자를 `0`으로 나누면 `-infinity`로 나온다.
- 또한 숫자가 아닌 종류를 연산한다면 `NaN (not a number)`값이 나온다.
- 자바스크립트 기존 숫자 범위를 더 늘리고 싶으면 숫자 맨 뒤에 `n`을 쓴다.<br/>
그러면 알아서 숫자범위를 늘리게 된다 `(big int)` 123436435435n

<br/>

### 31. rest 파라미터와 spread 연산자
1. `rest` 파라미터<br/>
함수의 인자를 여러개로 넣어보낼때 `function(...object) {}` 로 받으면 배열로 반환이 된다.

2. `spread` 연산자<br/>
배열을 합치거나, 풀어쓸 수 있다.

```javascript
console.log(...arr);  //배열 풀기
const newArr = [...arr] //배열 풀어서 다시 새배열에 넣기
const newArr = [...arr1, ...arr2] //배열 합치기 << concat을 대체가능하다.
```
<br/>

### 32. Node.js
`javascript`를 브라우저 밖에서 돌릴수 있는 자바스크립트 실행환경, 그래서 서버를 만들 수 있다.

<br/>

### 33. 브라우저 렌더링의 과정
1. `Loader` 가 서버로 부터 정보들을 불러온다.<br/>
2. 파싱을 통해 문서를 `DOM` 트리로 만든다.<br/>
3. `DOM` 트리가 구축되는 동안, 브라우저는 `render` 트리를 구축한다.<br/>
4. `CSS` 설정/레이아웃 위치 지정한다.<br/>
5. `rendering` 트리가 그려진다.
 
<br/>

### 34. MVC 패턴
시각적인 부분만 수정하려면 `view`에 해당하는 부분만 수정하면 되고<br/>
시각적인 부분과 관계 없이 데이터 처리 부분만 수정하려면 `model` 부분만,<br/>
프로그램간 연결과 제어를 수정하려면 `controller` 부분만 수정하면 되는 방식이다.

- M) `model` - 데이터를 처리하는 역할
- V) `view` - 사용자가 보는 화면
- C) `controller` - 각 요소들을 연결하고 데이터와 시각적 부분의 연결등을 관리한다

> 분리되어있어 유지보수가 편하고 어플리케이션의 확장성과 유연성이 늘어나고 중복코딩의 문제점이 사라진다.<br/>
유저 인터페이스와 비지니스 로직이 분리된다.

<br />


### 35. event bubbling
`DOM` 요소에서 `event`가 발생 되면 타겟페이즈까지 `event` 처리를 시도한 다음, 해당 `event`가 부모에게 `bubbling` 되고 부모에서 같은 이벤트가 발생한다.<br/>
이 `bubbling`은 요소의 최상단 부모요소인 `document`까지 계속적으로 발생시킨다.<br/>
이 모양이 물 안에서 버블이 상단으로 올라가는 모습을 닮았다고 하여 `event bubbling` 이라고 부른다.

<br />

### 36. event loop
- `event loop`는 `call stack`을 계속 모니터링 하고 있다.
- `Task que, Micro Task que, render`를 감시하며 수행할 작업이 있는지 확인한다.
- `callstack`이 비어있고 `task que`에서 콜백함수가 있는경우는 `que`에서 제거되고 실행될 `call stack`으로 보낸다.
- 다만 여기서 `Micro Task que`는 모든 실행이 끝나기 전까지 `call stack`으로 돌아오지 않는다.
- `Task que`는 한개만 실행하고 다시 `event loop`가 돌기 때문에 다른 부분은 작동할 수 있다.

<br />

### 37. 함수형 프로그래밍
성공적인 프로그래밍을 위해 `순수 함수`를 만들고 `모듈화` 수준을 높이는 프로그래밍 패러다임이다.<br/>
함수형 프로그래밍은 조합성을 강조하고, 이러한 순수함수들의 조합으로 프로그래밍을 한다.<br/>
<br/>
조합성을 강조한다는 것은 모듈화 수준을 높인다는 것이다.<br/>
순수함수로 모듈화 수준을 높이게 되면 오류는 적고, 안정성이 높아지고, 모듈화 수준이 높은 프로그래밍을 할 수 있다.<br/>
모듈화 수준이 높으면, 재사용성이 높고 기획 변경에 대한 대응력이 좋은 프로그래밍을 할 수 있다.<br/>

순수함수

- `부수효과(side effect)`가 없는 함수이다.
- 수학적 함수이다.
- 들어온 인자가 같으면 항상 같은 값을 리턴하는 함수이다. (리턴필수)
- 함수가 받은 인자 외에 다른 어떤 `외부의 상태에 영향을 끼치지 않는` 함수이고
- 즉, 리턴값 외에는 외부와 소통하지 않는 것을 말한다.

``` javascript
function add(a, b) {
  return a + b;
}

console.log(add(10, 5));
```

여기서 `add`는 순수함수이다.<br/>
`add(10, 5)` 로 항상 동일한 입력을 주면 동일한 아웃풋을 리턴하기 때문이다.<br/>
그리고 함수가 리턴값을 만드는 것 외에 외부의 상태에 영향을 미치지 않기 때문에 부수효과가 없다.<br/>

``` javascript
var c = 10;
function add2(a, b) {
  return a + b + c;
}
console.log(add2(10, 2));
c = 20;
console.log(add2(10, 2));
```

이 상황에서 `add2`는 순수함수가 아니다.<br/>
외부의 상태 값이 함수 내부에도 영향을 끼칠 수 있어 `side effect`가 일어날 수 있다.<br/>
만약 `c`가 변수가 아니고 상수로서 존재하게 된다면 `add2`도 순수함수가 될 수 있다.<br/>

``` javascript
var c = 20;
function add3(a, b) {
  c = b;
  return a + b;
}
```

리턴 값으로 소통하는 것 외에 외부 상태에 영향을 미치는 함수이기 때문에 이 예제도 순수함수라고 할 수 없다.<br/>
<br />

``` javascript
var obj1 = {val: 10}
function add5(obj, b) {
  return {val: obj.val + b}
}
```

`add5`는 값을 변경하지도 않고, 외부의 상태를 변경하고 있지도 않는다. 새로운 객체를 반환했기 때문이다.<br/>
그렇기 때문에 `add5`는 순수함수라고 말할 수 있다.<br/>

<br/>

일급함수

- 함수를 값으로 다룰 수 있는 개념이다.
- 자바스크립트에서는 변수에 함수를 담을 수 있다.
- 함수가 함수를 인자로 받을 수 있다.

```javascript
var f1 = function(a) {return a * a};
console.log(f1);

var f2 = add;
console.log(f2);
```

```javascript
/* add_maker */
function add_maker(a) {
  return function(b) {
    return a + b;
  }
}
var add10 = add_maker(10);
add10(20);
```

== 이 값은 30이 된다.

일단 `var add10 = add_maker(10)`가 실행되면

```javascript
function add_maker(10) {
  return function(b) {
    return a + b;
  }
}
```

`add_maker`에 `10`을 넣어 실행이 되고 `add_maker(10)`라는 것은 함수를 리턴해준다.

```javascript
var add10 = return function(b) {
return 10 + b;
}
```

즉 `var add10 = add_maker(10)`는 다시말하면 이렇게 바꿀 수 있다.<br/>
`add10` 도 함수가 될 수 있으니 `add10(20)`은 `b`에 `20`이 들어가 계산을 하게 된다.

```javascript
return function(b) {
  return a + b;
}
```
이 부분은 외부에서도 계속 쓰이고 있는 상황이기 때문에 `클로저`가 된 상황이고,<br/>
또한 함수가 함수를 값으로 다루기 때문에 `일급함수`이기도 하다.

<br/>


<br/><br/>
> 참조 링크<br/>
https://poiemaweb.com/es6-arrow-function<br/>
https://poiemaweb.com/js-spa<br/>
https://sunnykim91.tistory.com/121<br/>
https://www.youtube.com/watch?v=VEAUpHod4cg<br/>
https://velog.io/@kler/TIL4-%EB%A1%9C%EC%BB%AC%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80-%EC%84%B8%EC%85%98%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80-%EC%BF%A0%ED%82%A4-%EC%A0%95%EB%A6%AC<br/>
https://uwostudy.tistory.com/55<br/>
https://eodevelop.tistory.com/68<br/>
https://ithub.tistory.com/223<br/>
