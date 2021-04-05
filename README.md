# LearnJavaScript 

## 목차
- [this](#this)
- [data type](#data-type)
- [call, apply, bind](#call,-apply,-bind)
- [arrow function](#arrow-function)
- [arrow function을 사용해서는 안되는 경우](#arrow-function을-사용해서는-안되는-경우)

## 내용

### this
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

> 또한 화살표 함수는 `call, apply, bind` 메소드를 사용하여 `this`를 변경할 수 없다.


``` javascript

```

> "use strict" 모드에서는 window 객체를 this를 통해 참조할 수 없기 때문에 undefined가 나올 수 있다.

<br />

### call, apply, bind

이는 함수에 this를 바인딩 하기 위한 방법이다.
- call은 this를 바인딩 하면서 두번째 인자를 , 쉼표로 이어서 호출한다.
- apply는 call과 동일하지만 두번째 인자를 [a,b,c,d] 배열로 호출한다.
- bind는 함수를 호출하는 것이 아닌 this가 바인딩 된 새로운 함수를 리턴한다.

<br/>

### arrow function
화살표 함수는 Lexical this를 지원하므로 콜백 함수로 사용하기 편리하다. 


### arrow function을 사용해서는 안되는 경우

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
메소드에 화살표 함수를 쓸 경우에는 window 전역을 가르키는데 그것이 "use strict" 모드에서는 undefined가 뜬다.

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

화살표 함수로 정의된 메소드를 prototype에 할당하는 경우에도 동일한 문제가 발생한다.

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
생성자 함수는 prototype 프로퍼티를 가지며 prototype 프로퍼티가 가리키는 프로토타입 객체의 constructor를 사용한다.
하지만 화살표 함수는 prototype 프로퍼티를 가지고 있지 않다.

4. addEventListener의 콜백함수
addEventListener 함수의 콜백함수를 화살표 함수로 정의하면 this가 상위 컨텍스트인 전역 객체 window를 가리킨다.
따라서 일반 함수를 사용하여야 한다.

<br/>

### data type
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
  
### let, const, var의 차이점

- `let`과 `const`는 es5 이후에 나온 신문법이다.<br />
기존 변수와 상수를 구분하지 않고 사용하던 `var`를 대신하기 위해 나왔다.
- `let`, `const`과 `var`는 스코프가 다르다.<br/>
`let`, `const`는 실행 컨텍스트가 블럭 스코프를 지원하며 `{}` var는 함수스코프를 지원한다. `function {}`
- `var`는 호이스팅으로 올라가 선언하기 전에도 값을 찍을 수 있다.<br/> 값이 할당되지 않았기 때문에 `undefined`가 뜬다.<br/>
반면 `let`과 `const`는 호이스팅을 지원하지만 막아두어서 에러가 발생한다.


> 참조 링크
https://poiemaweb.com/es6-arrow-function
