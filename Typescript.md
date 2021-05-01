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
- [1. Typescript란?](#1-typescript란)
- [2. Typescript 기본타입](#2-typescript-기본타입)
- [](#)
- [](#)
- [](#)
- [](#)
- [](#)

<br/>

## 내용

### 1. Typescript란?

`typescript`는 오픈소스 언어이며,  `javascript` 위에서 동작한다. (확장된 개념)<br/>
세계에서 가장 많이 쓰이고 있는 툴이며 `type`의 정의를 더해준다.<br/>
<br/>
typescript에서 type을 작성하는 것은 `선택요소`이다, 즉 type을 `작성하지 않아도 된다.`<br/>
<br/>
모든 유효한 javascript 코드는 typescript 코드라고 말할 수 있다. <br/>
왜냐면 typescript는 `javascript를 기반으로 만들어진 언어`이기 때문이다.<br/>
<br/>
typescript 코드는 javascript코드로 `변환`이 되는데 typescript `컴파일러`를 사용하거나 `바벨`을 이용할 수 있다.<br/>
이 변환한 코드는 javascript가 동작하는 어떤 곳에서도 사용할 수 있다.<br/>
<br/>
typescript를 사용하기 위해서 꼭 전부를 typescript로 바꿀 필요가 없다.<br/>
typescript가 `필요한 부분에만 사용`할 수도 있다.

<br/>

### 2. Typescript 기본타입

타입스크립트로 변수나 함수와 같은 자바스크립트 코드에 타입을 정의할 수 있다.<br/>
타입스크립트의 기본 타입에는 크게 12가지가 있다.<br/>

- Number
- String
- Boolean
- Object
- Array
- Tuple
- Enum
- Any
- Void
- Null
- Undefined
- Never

> :를 이용하여 자바스크립트 코드에 타입을 정의하는 방식을 `타입 표기(Type Annotation)`라고 한다.


#### 1. Number

```typescript
let num: number = 1;
```

<br />

#### 2. String

```typescript
let str: string = "Red";
```

string type에 템플릿 문자열도 지원한다.

<br />

#### 3. Boolean

```typescript
let isLoggedIn: boolean = false;
```

<br />

#### 4. Array

```typescript
let fruits: string[] = ['Apple', 'Banana', 'Mango'];
// Or
let fruits: Array<string> = ['Apple', 'Banana', 'Mango'];
```

> 문자열만 있는 배열을 선언하고 싶을때 `String[]` 으로 작성하거나 제네릭 방식인 `Array<string>`으로 작성할 수 있다.

<br/>

```typescript
// 다중타입(문자열과 숫자를 동시에 가지는) 배열
let array: (string | number)[] = ['Apple', 1, 2, 'Banana'];
// Or
let array: Array<string | number> = ['Apple', 1, 2, 'Banana'];
```

> 유니언 타입 (|)을 이용해 다중타입을 가지게 할 수 있다.

<br/>

#### 5. tuple

```javascript
let student: [string, number];
student = ["ye-r1", 25]; // [string, number]
```

> 튜플은 배열의 `길이가 고정`되고 각 요소의 `타입이 지정`되어 있는 배열 형식을 의미한다.

tuple을 사용하는 것을 권장하지 않는다.<br/>
값을 출력할 때 `student[0]`처럼 가독성이 떨어지고 불편하기 때문이다.<br/>
tuple을 object나 class 형태로 사용한다면 `student.name` 처럼 명시적으로 접근할 수 있기 때문에, 되도록이면 다른 방식으로 접근하는 것이 좋다.<br/>

<br/>

**구조분해할당** <br/>

하지만 위의 것들을 사용하지 않고 명시적으로 사용할 수 있는 방법이 있는데, 바로 `구조분해할당 (object destructuring)` 이다.<br/>

```javascript
const [name, age] = student;
```

위와같이 `student[0]`, `student[1]`의 배열을 `명시적으로 선언`하여 가져올 수 있다.<br/>

```javascript
const [count, setCount] = useState();
```

구조분해할당은 `react useState`에서도 볼 수 있는데, `[count,setCount]`는 배열의 0번째 값과 1번째 값을 가져온 것이다.<br/>
하지만 `interface, class, type alias`를 이용하여 가져올 수 있음에도 불구하고 tuple을 사용하는 것은 지양해야한다.

<br />

#### 6. Enum

특정 값(상수)들의 집합을 의미한다.<br/>
타입스크립트에서는 문자형 이넘과 숫자형 이넘을 지원한다.


**숫자형 이넘**<br/>
```typescript
enum Direction {
  Up = 1,
  Down,
  Left,
  Right
}
```
`Up: 1 / Down: 2 / Left: 3 / Right: 4`<br/>
숫자형 이넘을 선언할 때 초기 값을 주면 초기 값부터 차례로 1씩 증가한다.<br/>

```typescript
enum Direction {
  Up, // 0
  Down, // 1
  Left, // 2
  Right // 3
}
```

초기 값을 주지 않으면 0부터 차례로 1씩 증가한다.


```typescript
enum Response {
  No = 0,
  Yes = 1,
}

function respond(recipient: string, message: Response): void {
  // ...
}

respond("ye-r1", Response.Yes);
```

```typescript
enum Wrong {
  A = getSomeValue(),
  B, // Error, 초기화가 필요합니다.
}
```
선언할 때 만약 이넘 값에 다른 이넘 타입의 값을 사용하면, 선언하는 이넘의 첫 번째 값에 초기화를 해줘야 한다.

<br/>

**문자형 이넘**<br/>
문자형 이넘은 숫자형 이넘과 개념적으로는 `거의 비슷`하다. 다만, `런타임`에서의 미세한 차이가 있다.<br/>
문자형 이넘은 이넘 값 `전부 다` 특정 `문자` 또는 다른 `이넘 값`으로 `초기화` 해줘야 한다.

```typescript
enum Direction {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT",
}
```

숫자형 이넘과는 다르게 `자동증가 (auto-incrementing)`가 없다.

**복합 이넘**<br/>

```typescript
enum BooleanLikeHeterogeneousEnum {
    No = 0,
    Yes = "YES",
}
```

기술적으로 이넘에 문자와 숫자를 혼합하여 생성할 순 있다.<br/>
하지만 이 방식을 추천하지 않기에 최대한 `같은 타입`으로 이루어진 이넘을 사용한다.
<br/>

**keyof**<br/>

```typescript
interface ICountries {
  KR: '대한민국',
  US: '미국',
  CP: '중국'
}
let country: keyof ICountries; // 'KR' | 'US' | 'CP'
country = 'KR'; // ok
```

인덱싱 가능 타입에서 `keyof`를 사용하면 `속성 이름(key)`을 `타입`으로 사용할 수 있다.<br/>
인덱싱 가능 타입의 속성 이름들이 `유니온 타입`으로 적용됩니다.
<br/>

```typescript
interface ICountries {
  KR: '대한민국',
  US: '미국',
  CP: '중국'
}
let country: ICountries[keyof ICountries]; //ICountries['KR' | 'US' | 'CP']
country = '대한민국'; // ok
```

또한 `keyof`를 통한 인덱싱으로 `타입의 개별 값`에도 `접근`할 수 있다.

<br />

#### 7. ani

```typescript
let anything: ani = 0;
// Or
let someArr: any[] = [0, {}, [], 'str', false];
```
`ani`는 `모든 타입`에 대해서 허용한다는 의미를 갖고 있다.<br/>
하지만 `any는` 가능하면 쓰지 않는 것이 좋다.

<br />

#### 8. void

```typescript
let unuseful: void = undefined;

function print():void {
}
```

아무것도 `return`하지 않을때 사용할 수 있고, 함수 기본이 void로 되어있어 생략할 수 있긴 하다.<br/>
변수에 쓰이는 경우는 드물다.

> 말 그대로 변수에 void를 쓰게 되면 아무것도 리턴하지 않는다, 즉 => undefined 밖에 할당되지 않기 때문에 쓰이지 않는다.

<br />

#### 9. null / undefined

```typescript
let name: undefined; 
let money: null; 
```
만약 undefined를 선언하면 `undefined` 말고 선언할 수 없다.<br/>
마찬가지로 null도 단독으로 선언하면 null 이외의 값을 가질 수 없다.

<br />

#### 10. Never

```typescript
function neverEnd(): never {
  while (true) {
  }
}
```
함수의 끝에 `절대 도달하지 않는다는 의미`를 지닌 타입이다.

<br />


#### union(|)

```typescript
let age: number | undefined;
type Direction = 'left' | 'right' | 'up' | 'down';
```

2개 이상의 type을 허용하는 경우 type을 `구분`하는 역할을 한다.<br/>
모든 가능한 `케이스`중에 발생할 수 있는 `딱 하나`를 담을 때 `union type`을 이용한다.

```typescript
function find(): number | undefined {
  return name;
}
```

`return` 값이 있으면 number를 리턴하고 찾지 못했으면 `undefined`를 리턴하게 만들 수 있다.

```typescript
// any를 사용하는 경우
function getAge(age: any) {
  // 에러 발생, age의 타입이 any로 추론되기 때문에 숫자 관련된 API를 작성할 때 코드가 자동 완성되지 않는다.
  age.toFixe();
}

// 유니온 타입을 사용하는 경우
function getAge(age: number | string) {
  if (typeof age === 'number') {
    // 정상 동작, age의 타입이 `number`로 추론되기 때문에 숫자 관련된 API를 쉽게 자동완성 할 수 있다.
    age.toFixed();
    return age;
  }
}
```

type을 추론하여 해당 타입과 관련된 API를 쉽게 `자동완성` 할 수 있다.

<br />

#### 인터섹션 타입(Intersection Type)

여러 타입을 모두 만족하는 하나의 타입을 의미한다.

```typescript
interface Person {
  name: string;
  age: number;
}
interface Developer {
  name: string;
  skill: number;
}
type Capt = Person & Developer;
```

Capt 타입은 Person 타입과, Developer 의 타입을 `&` 연산자를 이용하여 합친  할당한 코드이다.

```typescript
{
  name: string;
  age: number;
  skill: string;
}
```

이처럼 `&` 연산자를 이용해 `여러 개의 타입 정의`를 `하나로 합치는 방식`을 `인터섹션 타입` 정의 방식이라고 한다.

<br/>

**union 사용시 주의할점**<br/>

```typescript
interface Person {
  name: string;
  age: number;
}
interface Developer {
  name: string;
  skill: string;
}
function introduce(someone: Person | Developer) {
  someone.name; // O 정상 동작
  someone.age; // X 타입 오류
  someone.skill; // X 타입 오류
}
```

> 유니온 타입은 A도 될 수 있고 B도 될 수 있다고 생각하면,<br/>
파라미터의 타입이 Person도 되고 Developer도 될테니 함수 안에서<br/>
당연히 이 `인터페이스들이` 제공하는 `속성`들을 사용할 수 있겠지라고 생각할 수 있다.<br/>
하지만, 타입스크립트 관점에서는 introduce() 함수를 `호출하는 시점에`<br/>
Person 타입이 올지 Developer 타입이 올지 알 수가 없기 때문에<br/>
어느 타입이 들어오든 간에 오류가 안 나는 방향으로 타입을 `추론`하게 된다.<br/>
결과적으로 함수 안에서는 별도의 `타입 가드(Type Guard)`를 이용하여 타입의 `범위를 좁히지 않는 이상`<br/>
기본적으로는 두 타입에 `공통적으로 들어있는 속성만` `접근`할 수 있게 된다.

<br/>

#### function

```typescript
function sum(a: number, b: number): number {
  return a + b;
}
```

함수의 선언 방식에서 매개변수와 반환 값에 타입을 추가할 수 있다.<br/>
<br/>

**함수의 인자**<br/>
타입스크립트에서는 함수의 인자를 모두 필수 값으로 간주한다.<br/>
따라서, 함수의 매개변수를 설정하면 undefined나 null이라도 인자로 넘겨야하며, 컴파일러에서 정의된 매개변수 값이 넘어 왔는지 확인한다.

> 즉, 정의된 매개변수 값만 받을 수 있고 추가로 인자를 받을 수 없다.

#### this

```typescript
interface Vue {
    el: string;
    count: number;
    init(this: Vue): () => {};
}

let vm: Vue = {
    el: '#app',
    count: 10,
    init: function(this: Vue) {
        return () => {
            return this.count;
        }
    }
}
```

타입스크립트에서 자바스크립트의 this가 잘못 사용되었을 때 감지할 수 있다.

```typescript
class Handler {
    info: string;
    onClick(this: void, e: Event) {
        // `this`의 타입이 void이기 때문에 여기서 `this`를 사용할 수 없다.
        console.log('clicked!');
    }
}
```

만약 `this`를 사용하지 않는다면, `void` 타입을 선언할 수 있다.

<br />


#### interface

인터페이스는 상호 간에 정의한 약속 혹은 규칙을 의미한다.

```typescript
interface Todo {
  id: number;
  content: string;
  completed: boolean;
}

let todo: Todo;

// 설정된 todo는 Todo 인터페이스를 준수하여야 한다.
todo = { id: 1, content: 'typescript', completed: false };
```

- 일반적으로 타입 체크를 위해 사용되며 `변수`, `함수`, `class`에 사용할 수 있다.
- `여러가지 타입을 갖는 프로퍼티로 이루어진` 새로운 타입을 정의하는 것과 유사하고, 메소드의 `구현을 강제`하여 `일관성`을 `유지`할 수 있도록 하는 것이다.
- 인터페이스에 정의된 속성, 타입의 조건만 만족한다면 객체의 속성 `갯수가 일치하지 않더라도` 상관 없다.
- 인터페이스에 선언된 `속성 순서`를 지키지 않아도 된다.

```typescript
interface 인터페이스_이름 {
  속성?: 타입;
}
```

옵션(`?`)을 이용하면 필수로 존재하지 않아도 된다. <br />

**readonly**

```typescript
function printArr(fruits: readonly string[]) {
}

interface CraftBeer {
    readonly brand: string;
}
```

주어진 함수의 인자를 변경하고 싶지 않을때 `readonly`를 사용하여 타입을 `보장`받을 수 있다.<br/>
읽을 수만 있기 때문에 데이터를 `조작`한다면 `에러`가 발생한다. `(push, pop)`<br/>

> `readonly`를 사용하는 경우에는 `string[]` 처럼 표기할 수 있지만, `Array<string>`으로 표기할 수 없다.<br/>일관성을 위해 `string[]`과 같은 방식으로 통일하는 것이 좋다.


**읽기 전용 배열**

```typescript
let arr: ReadonlyArray<number> = [1,2];
```
배열을 선언할 때 `ReadonlyArray<T>` 타입을 사용하면 `읽기 전용 배열`을 생성할 수 있다.

<br />

**객체 선언의 타입 체크**<br/>

타입스크립트는 인터페이스를 이용하여 객체를 선언할 때 `엄격한 속성 검사`를 진행한다.

```typescript
interface CraftBeer {
  brand?: string;
}

function brewBeer(beer: CraftBeer) {
  // ..
}
brewBeer({ brandon: 'what' });  //error
```
위의 코드는 오탈자 점검 에러가 발생된다.

```typescript
let myBeer = { brandon: 'what' };
brewBeer(myBeer as CraftBeer);
```

이런 타입 추론을 무시하고 싶을때 as를 사용하여 타입을 단언한다.

```typescript
interface CraftBeer {
  brand?: string;
  [propName: string]: any;
}
```

인터페이스 정의하지 않은 속성들을 추가로 사용하고 싶을 때에 사용한다.

<br/>

**함수타입의 interface**

```typescript
//함수타입 interface 정의
interface login {
  (username: string, password: string): boolean;
}

//함수의 interface 사용
let loginUser: login;
loginUser = function(id: string, pw: string) {
    console.log('로그인 했습니다');
    return true;
}
```

<br/>

**클래스타입의 interface**

```typescript
interface CraftBeer {
  beerName: string;
  nameBeer(beer: string): void;
}

class myBeer implements CraftBeer {
  beerName: string = 'Baby Guinness';
  nameBeer(b: string) {
    this.beerName = b;
  }
  constructor() {}
}
```

**interface 확장**

```typescript
interface Person {
  name: string;
}
interface Developer extends Person {
  skill: string;
}
let fe = {} as Developer;
fe.name = 'josh';
fe.skill = 'TypeScript';
```

class 확장처럼 interface에도 확장해서 사용할 수 있다.

<br/>

**하이브리드 interface**

```typescript
interface CraftBeer {
  (beer: string): string;
  brand: string;
  brew(): void;
}

function myBeer(): CraftBeer {
  let my = (function(beer: string) {}) as CraftBeer;
  my.brand = 'Beer Kitchen';
  my.brew = function() {};
  return my;
}

let brewedBeer = myBeer();
brewedBeer('My First Beer');
brewedBeer.brand = 'Pangyo Craft';
brewedBeer.brew();
```

인터페이스에 여러 가지 타입을 조합하여 만들 수 있다.

<br/>


#### unknown

```typescript
let notSure: unknown;
```

어떤 데이터의 종류가 담길지 알 수 없는 type이 된다.<br/>
할당해도 다른 데이터로 다시 담을 수 있다.<br/>
하지만 typescript 의도와는 다를 수 있으니, 가능하면 쓰지 않는 것이 좋다.

<br />

#### 타입 별칭 (Type Alias)

```typescript
// 타입 앨리어스
type Person = {
  name: string,
  age?: number
}

or

//인터페이스
interface Person {
  name: string,
  age?: number
}

// 빈 객체를 Person 타입으로 지정
const person = {} as Person;
person.name = 'Lee';
person.age = 20;
person.address = 'Seoul'; // Error
```


타입 앨리어스는 `새로운 타입`을 `정의`한다.<br/>
타입으로 사용할 수 있다는 점에서 타입 앨리어스는 인터페이스와 `유사`하다.<br/>

> 하지만 타입 앨리어스는 `원시값, 유니온 타입, 튜플 등`도 타입으로 `지정`할 수 있다.

```typescript
// 문자열 리터럴로 타입 지정
type Str = 'Lee';

// 유니온 타입으로 타입 지정
type Union = string | null;

// 문자열 유니온 타입으로 타입 지정
type Name = 'Lee' | 'Kim';

// 숫자 리터럴 유니온 타입으로 타입 지정
type Num = 1 | 2 | 3 | 4 | 5;

// 객체 리터럴 유니온 타입으로 타입 지정
type Obj = {a: 1} | {b: 2};

// 함수 유니온 타입으로 타입 지정
type Func = (() => string) | (() => void);

// 인터페이스 유니온 타입으로 타입 지정
type Shape = Square | Rectangle | Circle;

// 튜플로 타입 지정
type Tuple = [string, boolean];
const t: Tuple = ['', '']; // Error
```

<br/>

#### 제네릭(Generic)
`재사용을 목적`으로 함수나 클래스의 `선언 시점`이 아닌, `사용 시점`에 `타입`을 `선언`할 수 있는 방법이다.

```typescript
function toArray<T>(a: T, b: T): T[] {
  return [a, b];
}

toArray<number>(1, 2);
toArray<string>('1', '2');
toArray<string | number>(1, '2');
toArray<number>(1, '2'); // Error
```

- 함수 이름 우측에 `<T>`를 작성해 시작한다.
- `T`는 `타입 변수(Type variable)`로 `사용자가 제공한 타입`으로 `변환`될 식별자다.
- 의도적으로 `Number`와 `String` 타입을 `동시에 받을 수 있다.` (유니언을 사용하지 않으면 에러가 발생한다)
- 타입 변수는 `매개 변수`처럼 `원하는 이름`으로 `지정`할 수 있다.


<br/><br/>
> 참조 링크<br/>
https://heropy.blog/2020/01/27/typescript/<br/>
https://poiemaweb.com/typescript-interface<br/>
https://poiemaweb.com/typescript-alias<br/>
https://joshua1988.github.io/ts/guide/basic-types.html<br/>
