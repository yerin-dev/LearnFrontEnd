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

- [1. "use strict"](#1-use-strict)
- [2. event bubbling](#2-event-bubbling)
- [3. event loop](#3-event-loop)
- [4. script 속성 async, defer](#4-script-속성-async-defer)
- [5. Node.js](#5-nodejs)
- [6. this](#6-this)
- [7. call, apply, bind](#7-call-apply-bind)
- [8. arrow function](#8-arrow-function)
- [8-1. arrow function을 사용해서는 안되는 경우](#8-1-arrow-function을-사용해서는-안되는-경우)
- [9. data type](#9-data-type)
- [10. let, const, var의 차이점](#10-let-const-var의-차이점)
- [11. null, undefined](#11-null-undefined)
- [12. hoisting](#12-hoisting)
- [13. curring 함수](#13-curring-함수)
- [14. HOF (High Order Function) 고차함수](#14-hof-high-order-function-고차함수)
- [15. ajax, fetch, axios](#15-ajax-fetch-axios)
- [16. promise, async await](#16-promise-async-await)
- [17. number](#17-number)
- [18. rest 파라미터와 spread 연산자](#18-rest-파라미터와-spread-연산자)
- [19. 함수형 프로그래밍](#19-함수형-프로그래밍)
- [20. 함수](#20-함수)
- [21. 객체](#21-객체)
- [22. 숫자형](#22-숫자형)
- [23. 배열](#23-배열)
- [24. prototype](#24-prototype)
- [](#)
- [](#)
- [](#)
- [](#)

<br/>

## 내용

### 1. "use strict"
자바스크립트 엄격모드<br/>
비 상식적인 구문을 에러시킨다.<br/>
"보안" 자바스크립트를 작성하는 쉬운 방법이다.

<br/>

### 2. event bubbling
`DOM` 요소에서 `event`가 발생 되면 타겟페이즈까지 `event` 처리를 시도한 다음, 해당 `event`가 부모에게 `bubbling` 되고 부모에서 같은 이벤트가 발생한다.<br/>
이 `bubbling`은 요소의 최상단 부모요소인 `document`까지 계속적으로 발생시킨다.<br/>
이 모양이 물 안에서 버블이 상단으로 올라가는 모습을 닮았다고 하여 `event bubbling` 이라고 부른다.

<br />

### 3. event loop
- `event loop`는 `call stack`을 계속 모니터링 하고 있다.
- `Task que, Micro Task que, render`를 감시하며 수행할 작업이 있는지 확인한다.
- `callstack`이 비어있고 `task que`에서 콜백함수가 있는경우는 `que`에서 제거되고 실행될 `call stack`으로 보낸다.
- 다만 여기서 `Micro Task que`는 모든 실행이 끝나기 전까지 `call stack`으로 돌아오지 않는다.
- `Task que`는 한개만 실행하고 다시 `event loop`가 돌기 때문에 다른 부분은 작동할 수 있다.

<br/>

### 4. script 속성 async, defer

`<script async>`<br/>
파싱을 하고 있는 도중에 동시에 다운받고 다운이 끝나면 파싱을 잠시 중단하고 실행한다.<br/>
하지만 이는 `파싱 중 실행구문을 실행`시킨것이기에 조작하려는 시점에 `html`들이 없을 수도 있어 위험할 수 있다.<br/>
실행구문을 불러오는 중에는 `html 파싱이 중단`되므로 여전히 페이지 로딩은 오래걸린다.<br/>
순서의 의존적인거라면 `async` 옵션은 로딩에 문제가 걸릴 수 있다.<br/>
<br/>
`<script defer>`<br/>
파싱을 하는 중에 `동시에 다운받고` 기다리다가 `html파싱이 완료`되면 실행한다.<br/>
파싱하는 `동안` 다운받고 `html파싱이 완료`된 후에 실행이 되기 때문에 좋다.<br/>

<br/>

### 5. Node.js
`javascript`를 브라우저 밖에서 돌릴수 있는 자바스크립트 실행환경, 그래서 서버를 만들 수 있다.

<br/>

### 6. this
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

### 7. call, apply, bind

이는 함수에 `this`를 바인딩 하기 위한 방법이다.
- `call`은 `this`를 바인딩 하면서 두번째 인자를 `,` 쉼표로 이어서 호출한다.
- `apply`는 `call`과 동일하지만 두번째 인자를 `[a,b,c,d]` 배열로 호출한다.
- `bind`는 함수를 호출하는 것이 아닌 `this`가 바인딩 된 새로운 함수를 리턴한다.

<br/>

### 8. arrow function
화살표 함수는 `Lexical this`를 지원하므로 콜백 함수로 사용하기 편리하다. 

<br/>

### 8-1. arrow function을 사용해서는 안되는 경우

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

### 9. data type

자바스크립트의 데이터 타입에는 크게 두가지로 나눌 수 있다.

1. 원시형

  `string, number, boolean, null, undefined`
  
  - 원시형은 데이터의 값 그 자체를 의미한다.
  - 용량이 작아 자체를 저장하며, 데이터의 값이 변경될 때에는 주소 자체를 변경시킨다.
  - 이로 인해서 자바스크립트의 원시형은 불변성을 띄는 데이터 타입이다.
  
2. 참조형

  `function, array, object`
  
  - 참조형은 용량이 커 데이터가 담긴 주소값으로 이루어진 `묶음`을 저장하며, 가변값이다.
  - 참조형 데이터의 `프로퍼티 재할당`시, 이전 데이터는 `가비지 컬렉터`의 `수거대상`이 되며, `런타임`이 돌다가 `자동으로 수거`하여 `빈공간`이 된다.

<br />
  

**메모리와 데이터**<br/>
`0` 또는 `1`로 표현할 수 있는 하나의 `메모리 조각`을 `비트(bit)`라고 한다.<br/>
각 비트는 고유한 식별자를 통해 위치를 확인할 수 있다.<br/>
`bit`를 일일히 찾는 것은 비효율적이기 때문에 `한 단위를 묶어` 위치를 확인하게 되는데,<br/>
그 결과로 `8개의 bit`로 이루어진 `1바이트(bite)`라는 단위가 생기게 되었다. 즉, 1`bite`는 8`bit`로 이루어져 있다.<br/>
<br/>
자바스크립트의 숫자형은 8`바이트`의 메모리 공간을 할당하며, 정수형과 부동소수형을 구분하지 않는다.<br/>
모든 데이터는 bite단위의 식별자, 즉 `메모리주소값`을 통해 서로 연결된다.

<br/>

**변수**<br/>
변수는 변할 수 있는 `수`를 말한다.<br/>
수학 용어를 차용했기 때문에 숫자를 의미하는 `수`가 붙었을 뿐, 반드시 `숫자`여야 하는 것은 아니다.<br/>
`variable`은 `변할 수 있다` 라는 형용사이지만 컴퓨터 용어에서 명사로 확장시켜, `변할 수 있는 무언가`를 뜻하게 되었다. => 즉 `변할 수 있는 data`를 뜻하게 된다.

<br/>

**식별자**<br/>
식별자는 어떤 데이터를 `식별하는 데 사용하는 이름`, 즉 `변수명`을 뜻한다.

<br/>

**데이터 할당**<br/>
`var a = "abc";`<br/>

위와 같은 예제가 있을때, 컴퓨터는 데이터를 `a`라는 변수에 `직접 저장`하지 않는다.<br/>
데이터를 저장하기 위한 `별도의 메모리 공간`을 다시 `확보`해서 `문자열을 저장`하고, 그 `주소값`을 변수에 저장하는 식으로 이루어진다.<br/>
<br/><br/>
그렇다면 왜 별도로 나눠진 공간을 사용하게 되는 것일까?<br/>
`숫자형` data는 `8바이트`의 공간을 가지고 있다. 반면 `문자열`은 특별히 정해진 규격이 없이 `가변적인 용량`을 가질 수 있다.<br/>
값이 수정될 때 이미 확보된 공간에서 변환된 크기에 맞게 `공간을 늘리는 작업이 복잡`하기 때문에 효율적인 처리를 위해 `변수`와 `데이터`의 공간을 별도로 저장하여 `주소를 담는 것`이다.


<br/>

### 10. let, const, var의 차이점

- `let`과 `const`는 es5 이후에 나온 신문법이다.<br />
기존 변수와 상수를 구분하지 않고 사용하던 `var`를 대신하기 위해 나왔다.<br/>
- `let`, `const`과 `var`는 스코프가 다르다.<br/>
`let`, `const`는 실행 컨텍스트가 블럭 스코프를 지원하며 `{}` var는 함수스코프를 지원한다. `function {}`<br/>
- `var`는 호이스팅으로 올라가 선언하기 전에도 값을 찍을 수 있다.<br/> 값이 할당되지 않았기 때문에 `undefined`가 뜬다.<br/>
반면 `let`과 `const`는 호이스팅을 지원하지만 막아두어서 에러가 발생한다.

<br/>

### 11. null, undefined
- 값이 없는 것을 뜻한다.
- `var`, `let`과 같이 데이터에 값이 할당되지 않았을때 `undefined`가 기본으로 할당된다.
- 하지만 `null`은 의도적으로 값이 비어있음을 표현한 것이다.
- null/undefined는 메서드가 없다.
- `typeof null`시 object가 출력되는 오류가 있다. JS의 자체 버그라고 한다.
- null과 undefined를 `동등연산자(==)`로 비교하면 구분하지 못하기 때문에, `일치연산자(===)`로 비교하여야 정확한 비교가 가능하다.

<br/>

### 12. hoisting
데이터를 선언하기 전에 호출했을때 아래에 있는 선언부분이 최상단으로 올라가지는 현상이다.<br/>
함수 선언은 함수 몸체가 `hoisting` 되는 반면에, 변수 선언 상태로 작성된 함수는 변수 선언만 `hoisting` 된다.

<br/>

### 13. curring 함수
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

### 14. HOF (High Order Function) 고차함수

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

### 15. ajax, fetch, axios
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

### 16. promise, async await
`promise`는 비동기 동작 다루기 위한 오브젝트이다.
- 콜백지옥을 막아줄 수 있고, 비동기 데이터를 가지고 성공 - 실패를 제어할 수 있다.

`async await`
- 자바와 같이 동기적 코드 흐름으로 개발이 가능하다.
- 코드가 간결해지고, 가독성이 높아진다.
- try / catch로 에러를 핸들링할 수 있다.
- error가 어디서 발생했는지 알기 쉽다.

<br/>

### 17. number
- 자바스크립트는 `number` 종류가 하나만 있다.
- 다른 언어에서는 용량, 속성에 따라 다르게 선언해야한다.
- 하지만 자바스크립트에서는 굳이 `number`라고 선언하지 않아도 다이나믹하게 자기가 결정한다.
- 자바스크립트에서는 정수나 소수점 상관없이 `number`라고 알아서 정의가 된다.
- 숫자를 `0`으로 나누면 `infinity`로 나오고 음수의 숫자를 `0`으로 나누면 `-infinity`로 나온다.
- 또한 숫자가 아닌 종류를 연산한다면 `NaN (not a number)`값이 나온다.
- 자바스크립트 기존 숫자 범위를 더 늘리고 싶으면 숫자 맨 뒤에 `n`을 쓴다.<br/>
그러면 알아서 숫자범위를 늘리게 된다 `(big int)` 123436435435n

<br/>

### 18. rest 파라미터와 spread 연산자
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

### 19. 함수형 프로그래밍
성공적인 프로그래밍을 위해 `순수 함수`를 만들고 `모듈화` 수준을 높이는 프로그래밍 패러다임이다.<br/>
함수형 프로그래밍은 조합성을 강조하고, 이러한 순수함수들의 조합으로 프로그래밍을 한다.<br/>
<br/>
조합성을 강조한다는 것은 모듈화 수준을 높인다는 것이다.<br/>
순수함수로 모듈화 수준을 높이게 되면 오류는 적고, 안정성이 높아지고, 모듈화 수준이 높은 프로그래밍을 할 수 있다.<br/>
모듈화 수준이 높으면, 재사용성이 높고 기획 변경에 대한 대응력이 좋은 프로그래밍을 할 수 있다.<br/>

**순수함수**<br/>

- `부수효과(side effect)`가 없는 함수이다. (외부의 상태를 변경하거나 인자의 상태를 직접 변경하는 것)
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

### 20. 함수
함수는 세가지 방법으로 함수를 만들 수 있습니다.<br/>

1. 함수 선언문

```javasciprt
function sum(a) {
}
```

2. 함수 표현식
```javascript
let sum = function(a) {
};
```

3. 화살표 함수
```javascript
// 화살표(=>) 바로 리턴
let sum = (a) => a;

// 중괄호{}를 사용하면 본문에 여러 줄의 코드를 작성할 수 있음. => 중괄호는 개행 / return문이 꼭 있어야 한다.
let sum = (a) => {
  return a;
}

// 인수가 없는 경우
let sum = () => "a";

// 인수가 하나인 경우
let sum = a => a;
```
<br/>

### 21. 객체
객체는 몇 가지 특수한 기능을 가진 연관 배열이다.

- 원시형과 달리 다양한 `data`를 담을 수 있다.
- `key`로 구분된 데이터 집합이나 복잡한 개체를 저장할 수 있다.
- 객체는 중괄호를 이용해 만들 수 있는데 중괄호 안에는 `key`와 `value` 쌍으로 구성된 프로퍼티를 여러개 넣을 수 있다.

```javascript
  const user = {
    name: "no_name"
  };

  user.name = "ye-r1";
```

`const`로 선언된 객체는 수정될 수 있다.<br/>
`user` 라는 객체를 전체적으로 설정하려고 할때만 오류가 발생하고, 내부의 값을 변경하는것은 오류가 발생하지 않는다.

```javascript
  const user = {
    name: "no_name"
  };

  user[name] = "ye-r1";
```

**대괄호 표기법**<br/>

객체는 대괄호를 이용해 접근할 수 있다.

```javascript
let key = "name";

console.log(user[key]); // "ye-r1"
```

`대괄호`를 사용한 접근법은 사용자의 입력값에 따라 값이 변경될 수 있으나, `점 표기법`은 유동적인 값으로 변경할 수 없다.<br/>

**계산된 프로퍼티**<br/>
객체를 만들때 객체 리터럴 안에 프로퍼티 `key`가 `대괄호`로 둘러쌓여 있는 경우 이를 `계산된 프로퍼티` 라고 한다.

```javascript
let fruit = "apple";

let bag = {
  [fruit]: 5, // 프로퍼티 이름을 동적으로 받아 온다.
};

alert( bag.apple ); // fruit에 "apple"이 할당되었다면, 5가 출력된다.
```

```javascript
let fruit = "apple";
let bag = {
  [fruit + 'Juice']: 5 // bag.appleJuice = 5
};
```

- `대괄호` 안에는 `복잡한 표현식`이 올 수도 있습니다.
- `대괄호` 표기법은 프로퍼티 이름과 값의 `제약`을 없애주기 때문에 점 표기법보다 훨씬 강력합니다. 그런데 `작성하기 번거롭다는 단점`이 있습니다.

**단축 프로퍼티**<br/>

```javascript
const user = {
  name: name,
  age: age
}
```

```javascript
const user = {
  name,
  age
}
```

**프로퍼티 삭제**<br/>
`delete user.age;`<br/>
프로퍼티 앞에 `delete`를 붙이면 프로퍼티를 삭제할 수 있다.


프로퍼티 이름과 값이 `동일`한 경우에는 이처럼 `단축`하여 코드를 작성할 수 있다.<br/>

**in 연산자로 프로퍼티 존재 여부 확인하기**<br/>

> 자바스크립트 객체는 다른 언어와는 달리, 존재하지 않는 프로퍼티에 접근하려 해도 에러가 발생하지 않고 `undefined`를 반환한다.<br/>
이런 특징을 응용하면 프로퍼티 존재 여부를 쉽게 확인할 수 있다.

```javascript
alert( user.name === undefined ); // true일때 값이 존재하지 않는다는 것을 의미하게 된다.
```

```javascript
"name" in user  //true일때 값이 있다는 것을 의미하게 된다.
```
또한 `undefined`와 비교하는 것 이외에도 연산자 `in`을 사용하면 프로퍼티 `존재 여부`를 확인할 수 있다.

```javascript
let user = {
  name: undefined
};

alert( user.name ); // undefined
alert( "name" in user ); // true
```

> 만약 프로퍼티는 `있음에도` 불구하고 값이 `undefined`일때는 `undefined`로 프로퍼티의 존재 유무를 알 수 없다.<br/>
이럴때 `in` 연산자를 이용한다면 프로퍼티의 유무를 제대로 알 수 있다.


**for in 반복문**<br/>
`for in` 반복문을 사용하면 객체의 모든 `key`를 순회할 수 있다.

```javascript
const user = {
  name: "ye-r1",
  age: 25
};
for (let key in user) {
  console.log(key); // name, age
  console.log(user[key]); // "ye-r1", 25
}
```

`for문`처럼 반복문 안에 `변수를 선언` 했다.<br/>
없어도 작동하지만 작성해주는 것이 좋다.<br/>
또한 `key` 말고 다른 변수명을 사용해도 괜찮다.<br/>

**객체 정렬 방식**<br/>

```javascript
const user = {
  name: "ye-r1",
  age: 25
};
const code = {
  "82": "Korea",
  "44": "United Kingdom",
  "1": "USA"
};

for (let key in user) {
  console.log(key); // name, age
}

for (let number in code) {
  console.log(number); // 1, 44, 82
}
```

프로퍼티가 정수일 경우에 자동으로 `오름차순`으로 정렬되고, 정수가 아닌 경우에는 `작성한 순서대로` 프로퍼티가 나열된다.

```javascript
const code = {
  "+82": "Korea",
  "+44": "United Kingdom",
  "+1": "USA"
};

for (let number in code) {
  console.log(+number); // 82, 44, 1
}
```

오름차순을 막고 싶은 경우에는 이런식으로 `문자`로 만들어서 출력할때 `+`로 숫자형 `형변환`을 통해 나열할 수도 있다.

<br/>

### 22. 숫자형

**숫자를 입력하는 다양한 방법**<br/>

```javascript
let billion = 1e9;  // 10억, 1과 9개의 0
alert( 7.3e9 );  // 73억 (7,300,000,000)
```

숫자 값을 쓸때 0을 많이 사용해 표현하다 보면 잘못 입력하기 쉽기 때문에, 실제로는 이런 방법을 잘 사용하지 않는다.<br/>
그래서 대개는 `10억`을 나타낼 땐 `1bn`을 사용하고, `73억`을 나타낼 땐 `7.3bn`을 사용한다. 큰 숫자를 나타낼 땐 이런 방법이 주로 사용된다.<br/>
<br/>
자바스크립트에서도 숫자 옆에 `e`를 붙이고 `0의 개수`를 그 옆에 붙여주면 숫자를 줄일 수 있다.<br/>
즉, `e`는 `왼쪽의 수`에 e `오른쪽에 있는 수`만큼의 `10의 거듭제곱`을 곱하는 효과가 있다.<br/>
<br/>
`7.3e9 = 7.3 * 1,000,000,000` 와 같다.<br/>

```javascript
let ms = 1e-6; // 1에서 왼쪽으로 6번 소수점 이동, 0.000001;
```

반대로 작은 숫자를 표현할 때도 `e`를 사용할 수 있다.

<br/>

**어림수 구하기**<br/>

숫자를 다룰 때 가장 많이 사용되는 연산 중 하나이다.

`Math.floor`<br/>
소수점 첫째 자리에서 내림(`버림`)<br/>
3.1 => 3 / -1.1 => -2<br/>

`Math.ceil`<br/>
소수점 첫째 자리에서 `올림`<br/>
3.1 => 4 / -1.1 => -1<br/>

`Math.round`<br/>
소수점 첫째 자리에서 `반올림`<br/>
3.1 => 3 / 3.6 => 4 / -1.1 => -1<br/>

`Math.trunc` (ie 지원 x)<br/>
`소수부를 무시`.<br/>
3.1 => 3 / -1.1 => -1<br/>

**parseInt와 parseFloat**<br/>

> `parseInt`는 정수형 변환을 해주며, `parseFloat`는 실수형 변환을 한다.
단위나 통화기호 같은 문자열과 같이 사용했을때 숫자만 남겨준다.

```javascript
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12, 정수 부분만 반환한다.
alert( parseFloat('12.3.4') ); // 12.3, 두 번째 점 이후의 읽기를 중지한다.
```

```javascript
alert( parseInt('a123') ); // NaN, a는 숫자가 아니므로 처음부터 숫자를 읽는 것을 중지한다.
```

`parseInt`와 `parseFloat`가 읽을 수 있는 숫자가 없을 때에는 `NaN`을 반환한다.<br/>

**기타 수학 함수**<br/>

`Math.random()`<br/>
0과 1 사이의 `난수`를 반환한다 (1은 제외)<br/>

```javascript
alert( Math.random() ); // 0.1234567894322
alert( Math.random() ); // ... (무작위 수)
```

`Math.max(a, b, c...) / Math.min(a, b, c...)`<br/>
인수 중 `최대/최솟값`을 반환한다.

```javascript
alert( Math.max(3, 5, -10, 0) ); // 5
alert( Math.min(1, 2) ); // 1
```

`Math.pow(n, power)`<br/>
`n`을 `power`번 `거듭제곱`한 값을 반환한다.

```javascript
alert( Math.pow(2, 10) ); // 2의 10제곱 = 1024
```

<br/>

### 23. 배열

`큐(queue)`는 배열을 사용해 만들 수 있는 대표적인 자료구조로, 배열과 마찬가지로 순서가 있는 컬렉션을 저장하는 데 사용한다.<br/>
큐에서 사용하는 주요 연산은 다음과 같다.

- `push` – `맨 끝`에 요소를 `추가`한다.
- `shift` – 제일 `앞` 요소를 꺼내 `제거`한 후 남아있는 요소들을 앞으로 밀어준다.

> 큐는 이러한 특징을 줄여서 먼저 집어넣은 요소가 먼저 나오기 때문에 `선입선출(First-In-First-Out, FIFO)` 자료구조라고 부른다.


배열은 큐 말고도 `스택(stack)`이라 불리는 자료구조를 구현할 때도 쓰인다.<br/>
스택에서 사용하는 연산은 다음과 같다.

- `push` – `맨 끝`에 요소를 `추가`한다.
- `pop` – 스택 `끝` 요소를 `추출`한다.

> 반면 스택은 `후입선출(Last-In-First-Out, LIFO)`이라고 부른다.

`pop·push와 shift·unshift`<br/>
<br/>


`pop`<br/>
배열 `끝` 요소를 `제거`하고, 제거한 요소를 `반환`한다.<br/>
<br/>
`push`<br/>
배열 `끝`에 요소를 `추가`한다.<br/>

> fruits.push(...)를 호출하는 것은 fruits[fruits.length] = ...하는 것과 같은 효과를 보인다.

`shift`<br/>
배열 `앞` 요소를 `제거`하고, 제거한 요소를 `반환`한다.<br/>
<br/>
`unshift`<br/>
배열 `앞`에 요소를 `추가`한다.<br/>

> push와 pop은 빠르지만 shift와 unshift는 느리다.
<br/>

`splice`<br/>
배열에서 요소를 하나만 지우고 싶을때 사용한다.<br/>
`splice`는 `삭제`된 요소로 구성된 `배열`을 반환다.

```javascript
let arr = ["I", "go", "home"];

delete arr[1]; // "go"를 삭제한다.
alert( arr[1] ); // undefined
// --> arr = ["I",  , "home"];

alert( arr.length ); // 3
```
`delete`는 key를 이용해 해당 `키에 상응하는 값`을 지웠기 때문에 공간은 남아있게 된다.<br/>
하지만 `splice`는 요소 추가, 삭제 교체가 모두 가능하다.<br/>
<br/>
`arr.splice(index, deleteCount, elem1, ...)`<br/>

- 첫번째 인자는 첫 `시작`범위의 인덱스를 받는다.
- 두번째 인자는 `제거`하고자 하는 요소의 `갯수`를 받는다.
- 그 다음에는 제거한 자리에 `추가할 요소`를 적는다.

```javascript
let arr = ["I", "study", "JavaScript", "right", "now"];

let removed = arr.splice(0, 2);

alert( removed ); // "I", "study"
```

<br/>

**반복문**<br/>

`for문`<br/>

```javascript
let name = ["lee", "ye", "rin"];

for (let i = 0; i < name.length; i++) {
  console.log( name[i] );
}
```

가장 기본적인 반복문이다, 순회시엔 인덱스를 사용한다.<br/>

`for of 문`<br/>

```javascript
let name = ["lee", "ye", "rin"];

// 배열 요소를 대상으로 반복 작업을 수행한다.
for (let key of name) {
  console.log( key );
}
```

`for of`를 사용하면 현재 요소의 `인덱스`는 얻을 수 없고 `값`만 얻을 수 있다.<br/>
배열은 `객체형`에 속하므로 `for in`을 사용하는 것도 가능하지만 여러가지 문제가 있으므로 되도록이면 배열은 `for of`를 사용하는 것이 좋다.

<br/>

**유사배열**<br/>

```javascript
const array = [1, 2, 3];
const nodes = document.querySelectorAll('div');
const els = document.body.children;

Array.isArray(array); // true
Array.isArray(nodes); // false
Array.isArray(els); // false
```

직접 `배열 리터럴로` 선언한 array만 `배열`이다.<br/>
`Array.isArray` 이외에도 `instanceof`로도 판단할 수 있다.<br/>
배열과 유사배열을 구분해야 하는 이유는, 유사배열의 경우 `배열의 메서드`를 쓸 수 없기 때문이다.

```javascript
[].forEach.call(els, function(el) { console.log(el); });
```

이러한 방식으로 메서드를 빌려온다면, 유사배열에도 `forEach, map, filter, reduce` 등의 다른 배열 메서드를 사용할 수 있다.

```javascript
Array.from(nodes).forEach(function(el) { console.log(el) });
```

최신 자바스크립트에서는 `Array.from`으로 더 간단하게 할 수 있다.

<br/>

**includes**<br/>

`includes()` 메서드는 배열이 특정 요소를 포함하고 있는지 판별한 후 `boolean` 값으로 반환한다.

```javascript
const pets = ['cat', 'dog', 'bat'];
pets.includes('cat'); //true
pets.includes('at'); //false
```

> 문자나 문자열을 비교할 때, includes()는 `대소문자를 구분`한다.

**[].includes(탐색할 요소, 시작할 위치)** (Optional) <br/>

```javascript
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
[1, 2, NaN].includes(NaN); // true
```

- 이 배열에서 탐색할 요소의 시작할 위치를 정할 수 있다.
- 음의 값은 배열의 길이에서 음의 값을 더하여 검색한다.
- 기본값은 0 이다.
- 배열 객체가 되기 위한 `this` 값을 요구하지 않아, 유사배열 객체에 적용될 수 있다.
- ie를 지원하지 않는다.

<br/>

### 24. prototype
객체의 원형이라고 할 수 있다.<br/>
함수는 객체고 생성자로 사용될 함수도 객체다.<br/>
객체는 프로퍼티를 가질 수 있는데 프로퍼티인 prototype는 그 용도가 약속되어있는 특수한 프로퍼티이다.<br/>
prototype에 저장된 속성들은 생성자를 통해서 객체가 만들어질 때 그 객체에 연결된다.






<br/><br/>
> 참조 링크<br/>
https://ko.javascript.info<br/>
https://poiemaweb.com/es6-arrow-function<br/>
https://www.youtube.com/watch?v=VEAUpHod4cg<br/>
https://uwostudy.tistory.com/55<br/>
https://ithub.tistory.com/223<br/>
https://www.zerocho.com/category/JavaScript/post/5af6f9e707d77a001bb579d2<br/>
