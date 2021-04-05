# Learn Front-end

## 목차
- [1. this](#1-this)
- [2. call, apply, bind](#2-call-apply-bind)
- [3. arrow function](#3-arrow-function)
- [3-1. arrow function을 사용해서는 안되는 경우](#3-1-arrow-function을-사용해서는-안되는-경우)
- [4. data type](#4-data-type)
- [5. let, const, var의 차이점](#5-let-const-var의-차이점)
- [6. hoisting](#6-hoisting)
- [7. curring 함수](#7-curring-함수)
- [8. HOF (High Order Function) 고차함수](#8-HOF-High-Order-Function-고차함수)
- [9. Eslint](#9-Eslint)
- [10. Prettier](#10-Prettier)
- [11. Webpack](#11-Webpack)
- [12. CORS (Cross-Origin Resourse Sharing)](#12-CORS-Cross-Origin-Resourse-Sharing)
- [13. Rest API](#13-Rest-API)
- [14. JSX](#14-JSX)
- [15. FLUX](#15-FLUX)
- [16. 사이트 렌더링방식](#16-사이트-렌더링방식)
- [17. 리액트 성능개선 방법](#17-리액트-성능개선-방법)
- [18. null, undefined](#18-null-undefined)
- [19. ajax, fetch, axios](#19-ajax-fetch-axios)
- [20. promise, async await](#20-promise-async-await)
- [21. 프레임워크, 라이브러리](#21-프레임워크-라이브러리)
- [22. 함수형 컴포넌트, 클래스형 컴포넌트](#22-함수형-컴포넌트-클래스형-컴포넌트)
- [23. react](#23-react)
- []()
- []()
- []()
- []()
- []()

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
화살표 함수는 생성자 함수로 사용할 수 없다.
생성자 함수는 `prototype` 프로퍼티를 가지며 `prototype` 프로퍼티가 가리키는 프로토타입 객체의 `constructor`를 사용한다.
하지만 화살표 함수는 `prototype` 프로퍼티를 가지고 있지 않다.

4. addEventListener의 콜백함수
`addEventListener` 함수의 콜백함수를 화살표 함수로 정의하면 `this`가 상위 컨텍스트인 전역 객체 `window`를 가리킨다.
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
기존 변수와 상수를 구분하지 않고 사용하던 `var`를 대신하기 위해 나왔다.
- `let`, `const`과 `var`는 스코프가 다르다.<br/>
`let`, `const`는 실행 컨텍스트가 블럭 스코프를 지원하며 `{}` var는 함수스코프를 지원한다. `function {}`
- `var`는 호이스팅으로 올라가 선언하기 전에도 값을 찍을 수 있다.<br/> 값이 할당되지 않았기 때문에 `undefined`가 뜬다.<br/>
반면 `let`과 `const`는 호이스팅을 지원하지만 막아두어서 에러가 발생한다.

### 6. hoisting
데이터를 선언하기 전에 호출했을때 아래에 있는 선언부분이 최상단으로 올라가지는 현상이다.
함수 선언은 함수 몸체가 `hoisting` 되는 반면에, 변수 선언 상태로 작성된 함수는 변수 선언만 `hoisting` 된다.

### 7. curring 함수
커링 함수의 인자로 함수를 전달하면 기능이 추가된 새 함수로 반환할 수 있다.
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
이렇게 사용하게 되면 우리가 생각하는 실행방향은 -> 지만
사실상 함수가 실행하는 순서는 <- 거꾸로 실행되는 것이 헷갈릴 수 있다.

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
위에 있는 이 `compose`가 고차함수이다.
함수를 받아 함수를 반환한다.


<br />

### 9. Eslint
문법적오류나 잠재적 오류까지 찾아내고 오류의 이유를 볼 수 있게 해주는 도구 (ex. `const`의 사용을 `let`으로 제안해주는 것)

<br />

### 10. Prettier
정해진 규칙대로 코드를 예쁘게 변경해주는 도구 (ex. 들여쓰기나 따옴표) 

<br />

### 11. Webpack
`webpack`은 모듈 번들러로 파일 확장자에 맞는 로더에게 위임해 하나로 묶어서 최종 배포용 파일을 만들어준다.
`<script>` 태그가 여러개 있을 때 순서보장을 맞게 해준다.

<br />

### 12. CORS (Cross-Origin Resourse Sharing)
도메인 또는 포트가 다른 서버의 자원을 요청하면 발생 하는 문제 
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
- `react.createElement( )`을 생성하여 편하게 `html`으로도 작성 가능하게 한다.
`cra`를 하게 되면 `webpack`에서 바벨로 처리해준다.

<br/>

### 15.FLUX
- MVC 패턴의 문제점을 개선한 패턴이다.
- MVC 패턴으로 진행하게되면 규모가 커지면서 Model 관리가 어려워진다.
- 단방향 데이터 흐름을 띄는 아키텍쳐이다. (→ 추적이 쉽다, 관리하기 쉽다)
- UI 데이터만 전달받는다.
- UI 데이터 변경시 직접 `store`와 동기적으로 연결하지 않고, `action`을 일으켜 변경사항을 업데이트한다.


<br/>

### 16. 사이트 렌더링방식
`SSR`<br/>
- 페이지를 이동할때마다 서버에 요청한다. => 서버에서 렌더링
- 소스를 전부 불러오기 때문에 검색엔진 최적화에 좋다.
- 중복리소스와 자원낭비가 심하다.
- 초기구동속도가 비교적 빠르다
- 페이지 이동시 깜빡임이 있다.

`CSR`<br/>
- 필요한 데이터만 서버에 요청하기 때문에 비교적 트래픽 감소가 있다. => 클라이언트에서 렌더링
- 깜빡이지 않기에 사용자 경험이 올라간다. (`native app`과 동일한 사용경험을 준다.)
- 검색엔진을 최적화 하려면 따로 `SSR` 렌더링이 필요하다.
- `SPA`방식이라 한번에 필요한 데이터를 전부 가져와 초기 속도가 오래 걸린다.

<br/>

### 17. 리액트 성능개선 방법

- 첫 페이지 로딩 지연문제를 해결한다. => 첫 페이지의 `SSR` (Server Side Rendering)
- 컴포넌트 `lazy loading`을 추가한다.
- 이미지 `lazy loading`을 추가한다.
- 네트워크 탭의 성능을 추적한다.
- `Re-rendering`을 최소화시킨다.
- 중복계산을 줄인다 (`UseEffect`, `UseMemo`)
- 스켈레톤을 추가한다. (ui-ux 관점)

<br/>

### 18. null, undefined
- 값이 없는 것을 뜻한다.
- `var`, `let`과 같이 데이터에 값이 할당되지 않았을때 `undefined`가 기본으로 할당된다.
- 하지만 `null`은 의도적으로 값이 비어있음을 표현한 것이다.

<br/>

### 19. ajax, fetch, axios
`HTML` 페이지 전체가 아닌 일부분만 갱신할 수 있도록 `XMLHTMLRequest` 객체를 서버로부터 요청하는 자바스크립트 비동기 통신방식이다.
- ajax: Jquery를 사용해야한다, promise 기반이 아니다.
- fetch: ie를 제외한 대부분의 브라우저에서 IMPORT없는 Web API를 사용 가능, promise를 지원
- axios: node.js와 브라우저를 위한 비동기통신 라이브러리, fetch와 달리 ie11도 지원, promise를 지원

<br/>

### 20. promise, async await
`promise`는 비동기 동작 다루기 위한 오브젝트이다.
- 비동기 데이터를 가지고 성공 - 실패를 제어할 수 있다.then, catch

`async await`
- promise를 쉽게 사용하는 신문법이다.

<br/>

### 21. 프레임워크, 라이브러리
프레임 워크: 어플리케이션 개발을 위한 뼈대, 개발이 빨라진다.
라이브러리: 어플리케이션의 기능을 빠르게 구현 제공하는 기능, 기능이라 개발 자유도가 높다
<br/>

### 22. 함수형 컴포넌트, 클래스형 컴포넌트
함수형 컴포넌트: 짧은 코드로 구현 신문법, 메모리 자원 덜 사용, hook 지원으로 state관리 쉬움
클래스형: 클래스 문법 라이프사이클 state관리, 지금은 hook 지원 노필요, 유지보수때문 다알아야
<br/>

### 23. react
spa로 이루어진 프론트앤드 자바스크립트 라이브러리

<br/>

### 24.

<br/>

### 25.

<br/>

### 26.





<br />
<br />
<br />
<br />
<br />
<br />





<Br/>
<Br/>
<Br/>

> 참조 링크<br/>
https://poiemaweb.com/es6-arrow-function<br/>
https://sunnykim91.tistory.com/121<br/>
https://www.youtube.com/watch?v=VEAUpHod4cg<br/>
