# LearnJavaScript 

## 목차
- [JavaScript this](#javaScript-this)
- [제목2](#제목2)

## 내용

### javaScript this
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


### 제목2
