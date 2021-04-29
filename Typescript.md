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
- [2. Typescript 선언법](#2-typescript-선언법)
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

### 2. Typescript 선언법

**Number**

```typescript
let num: number;
let num: number = 1;
```
<br/>

**String**

```typescript
let str: string;
let str: string = "Red";
```

string type에 템플릿 문자열도 지원한다.

<br/>

**Boolean**

```typescript
let isOpened: boolean;
let isOpened: boolean = false;
```

<br/>

**Array**

```typescript
// 문자열만 가지는 배열
let fruits: string[] = ['Apple', 'Banana', 'Mango'];
// Or
let fruits: Array<string> = ['Apple', 'Banana', 'Mango'];
```

문자열만 있는 배열을 선언하고 싶을때 `String[]` 으로 작성하거나 `Array<string>`으로 작성할 수 있다.

<br/>

```typescript
// 다중타입(문자열과 숫자를 동시에 가지는) 배열
let array: (string | number)[] = ['Apple', 1, 2, 'Banana'];
// Or
let array: Array<string | number> = ['Apple', 1, 2, 'Banana'];
```

<br/>

```typescript
let someArr: any[] = [0, 1, {}, [], 'str', false];
```

배열이 가지는 항목의 값을 `단언`할 수 없다면 `any`를 사용할 수 있다.

<br/>

**readonly**

```javascript
function printArr(fruits: readonly string[]) {
}
```

주어진 함수의 인자를 변경하고 싶지 않을때 `readonly`를 사용하여 타입을 보장받을 수 있다.<br/>
읽을 수만 있기 때문에 데이터를 조작한다면 에러가 발생한다. (push,pop)<br/>
<br/>
또한 `readonly`를 사용하는 경우에는 `string[]` 처럼 표기할 수 있지만, `Array<string>`으로 표기할 수 없다.<br/>
일관성을 위해 `string[]`과 같은 방식으로 통일하는 것이 좋다.

<br/>

**tuple**

```javascript
let student: [string, number];
student = ["ye-r1", 25]; // 첫번째의 인자는 string을, 두번째의 인자는 number의 type이 된다.
```

기존 방식의 `string[]` 배열은 문자열만 가질 수 있는데, tuple을 사용하면 서로 다른 type을 가질 수 있다.<br/>
하지만 tuple을 사용하는 것을 권장하지 않는다.<br/>
값을 출력할 때 `student[0]`처럼 가독성이 떨어지고 불편하기 때문이다.<br/>
tuple을 object나 class 형태로 사용한다면 `student.name` 처럼 명시적으로 접근할 수 있기 때문에, 되도록이면 다른 방식으로 접근하는 것이 좋다.<br/>
<br/>
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


<br/>

**interface**

```javascript
interface Todo {
  id: number;
  content: string;
  completed: boolean;
}

let todo: Todo;

// 설정된 todo는 Todo 인터페이스를 준수하여야 한다.
todo = { id: 1, content: 'typescript', completed: false };
```

일반적으로 타입 체크를 위해 사용되며 `변수`, `함수`, `class`에 사용할 수 있다.<br/>
`여러가지 타입을 갖는 프로퍼티로 이루어진` 새로운 타입을 정의하는 것과 유사하고, 메소드의 `구현을 강제`하여 `일관성`을 `유지`할 수 있도록 하는 것이다.<br/>

```javascript
interface Todo {
  id: number;
  content: string;
  completed: boolean;
}

let todos: Todo[] = [];

function addTodo(todo: Todo) {
  todos = [...todos, todo];
}

// 설정된 todo는 Todo 인터페이스를 준수하여야 한다.
const newTodo: Todo = { id: 1, content: 'typescript', completed: false };
addTodo(newTodo);
console.log(todos)
// [ { id: 1, content: 'typescript', completed: false } ]
```

인터페이스를 사용하여 `함수 파라미터`의 타입을 선언할 수 있다.<br/>
이때 해당 함수에는 함수 파라미터의 타입으로 지정한 인터페이스를 준수하는 인수를 전달하여야 한다.<br/>
함수에 객체를 전달할 때 `복잡한 매개변수 체크`가 필요없어서 매우 `유용`하다.

<br/>

**ani**

```typescript
let anything: ani = 0;
```

`ani`는 아무 type이나 사용할 수 있다. <br/>
하지만 `any는` 가능하면 쓰지 않는 것이 좋다.


<br/>

**undefined / null**

```typescript
let name: undefined; 
let money: null; 
```
만약 undefined를 선언하면 `undefined` 말고 선언할 수 없다.<br/>
마찬가지로 null도 단독으로 선언하면 null 이외의 값을 가질 수 없다.

<br/>

**union(|)**

```typescript
let age: number | undefined;
```

2개 이상의 type을 허용하는 경우 type을 `구분`하는 역할을 한다.<br/>
null도 마찬가지로 사용할 수 있지만, 의미에 맞게 undefined를 더 많이 사용하는 편이다.

<br/>

**function**

```typescript
function find(): number | undefined {
  return name;
}
```

`return` 값이 있으면 number를 리턴하고 찾지 못했으면 `undefined`를 리턴하게 만들 수 있다.

<br/>

**void**

```typescript
function print():void {
}
```

아무것도 `return`하지 않을때 사용할 수 있고, 함수 기본이 void로 되어있어 생략할 수 있긴 하다.<br/>
변수에 쓰이는 경우는 드물다.
> 말 그대로 변수에 void를 쓰게 되면 아무것도 리턴하지 않는다, 즉 => undefined 밖에 할당되지 않기 때문에
쓰이지 않는다.

<br/>

**unknown**

```typescript
let notSure: unknown;
```

어떤 데이터의 종류가 담길지 알 수 없는 type이 된다.<br/>
할당해도 다른 데이터로 다시 담을 수 있다.<br/>
하지만 typescript 의도와는 다를 수 있으니, 가능하면 쓰지 않는 것이 좋다.

<br/>

**Type Alias**

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


<br/><br/>
> 참조 링크<br/>
https://heropy.blog/2020/01/27/typescript/<br/>
https://poiemaweb.com/typescript-interface<br/>
https://poiemaweb.com/typescript-alias<br/>
