# LearnJavaScript 

## 목차
- [1. JavaScript this](#javaScript-this)
- [2. 제목2](#제목2)

## 내용

### javaScript this
자바스크립트의 this는 호출하는 방법에 의해 결정이 된다.<br/>
누가 불렀는지에 따라서 this의 의미가 달라진다.

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


### 제목2
