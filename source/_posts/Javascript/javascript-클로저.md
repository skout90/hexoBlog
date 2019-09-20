---
title: Javascript 클로저(Closure)
categories:
  - Javascript
date: 2017-08-13 01:00:00
---

내부함수가 외부함수의 맥락(지역변수)에 접근할 수 있는 것을 가리킨다.

````javascript
function outterFunc() {  // 외부함수
  var title = 'lalala';
  function innerFunc() { // 내부함수
    alert(title);
  }
  innerFunc();
}
````

어떠한 함수가 있는데, 그 함수 안에서만 사용되는 함수가 있다. 이것을 내부함수로 선언한다면 , 가독성을 높이고 오류 가능성을 줄일 수 있다.

그리고 이때, **내부함수에서 외부의 함수의 지역변수에 접근 할 수 있는데 이것을 클로저(Closure)**라고 한다.

- **외부함수가 더 이상 사용되지 않는 경우에도, 내부함수가 외부함수의 지역변수에 접근할 수 있다.**

````javascript
function outterFunc() { // 외부함수
  var title ='외부함수의 지역변수';
  return function() {   // 내부함수
    console.log(title);
  }
}

var innerFunc = outterFunc();
innerFunc(); // 외부함수의 지역변수
````

내부 함수를 리턴함으로서, 외부함수가 사라졌음에도 불구하고, 외부함수의 지역변수에 접근이 가능하다.

> 아래 코드를 보자.

````javascript
var arr = [];
for (var i = 0; i < 5; i++) {
  arr[i] = function() {
    return i;
  }
}
for (var index of arr) {
  console.log(arr[index]()); // 5 5 5 5 5
}
````

만약 결과를, 0 1 2 3 4 가 나오도록 바꾸고 싶다면. 클로저를 사용해야 한다.

````javascript
var arr = [];
for (var i = 0; i < 5; i++) {
  arr[i] = function(id) { // 외부 함수를 익명함수로 선언후 인자를 넘겨 바로 실행
    return function() {   // 내부 함수를 리턴
      return id; 
    }
  } (i);
}
for (var index of arr) {
  console.log(arr[index]()); // 0 1 2 3 4
}
````

arr[0]의 외부함수의 지역변수는 실행당시 맥락(i=0)을 유지하고 있는다.



### 클로저의 구조

클로저로, 외부 함수의 스코프 변수에 접근 가능한 이유는, 내부 함수의 스코프 체인에 외부함수의 스코프가 포함되기 때문이다.

````javascript
function cCompFunc(pName) {   
    return function (o1, o2) {
        var v1 = o1[pName];
      	var v2 = o2[pName];
      	return v1 - v2;
    }
}

var compare = cCompFunc('name');
var result = compare({name:'Junho'}, {name: 'JJong'});
````

![img](https://i.imgur.com/tBVLpkB.png)

1. cCompFunc(외부함수)가 실행을 마치고 익명함수를 반환
2. 익명함수의 스코프 체인에는 외부함수의 활성화 객체, 전역함수가 포함
3. 익명함수는 외부함수의 변수 전체에 접근

> 익명함수의 스코프 체인에서 외부함수를 참조하고 있기 때문에, 외부함수의 활성화 객체는 가비지 컬렉션의 대상이 되지 않는다.

#### 내부 함수는 외부함수 변수에 저장된 마지막 값만 알 수 있음.

````javascript
function createFunc() {
  var result = [];
  for(var i = 0; i<10; i++) {
      result[i] = function() {
          return i;
      }
  }
  return result;
}
var a = createFunc();
a[0](); // 






a[0](); // 10
a[1](); // 10
````

- 모든 함수가 10을 반환, 모든 함수가 createFunc()의 활성화 객체의 같은 변수 i를 참조한다.

> 수정 버젼

````javascript
function createFunc() {
    var result = [];
    for(var i = 0; i<10; i++) {
        result[i] = function(num) {
              return function() {
                  return num; 
              };
        }(i);
    }
  	return result;
}
var a = createFunc();

a[0](); // 0
a[1](); // 1
````

function 함수를 한번 더 감싸고, 실행시킴으로써, num에는 i자체가 아니라 값이 복사되어 들어오게 된다. 내부함수에는 복사된 제각기 다른 num을 가지게 되어 의도한대로 값을 출력할 수 있다.

#### 클로저의 this 객체

this객체는 런타임에서 함수가 실행 중인 컨텍스트 객체를 가리킨다.

````javascript
var name = "Window";
var obj = { name: "Obj",
          	getNameFunc: function() {
            	return function() {
                    return this.name;
                }    
            }
          };
alert(obj.getNameFunc()); // Window
````

**익명함수는 외부 함수의 this****객체를 직접****적으로 접근할 수 없다.**

- 수정 버젼

````javascript
var name = "Window";
var obj = { name: "Obj",
          	getNameFunc: function() {
              	var that = this;
            	return function() {

                    return that.name;
                }    
            }
          };
alert(obj.getNameFunc()); // Obj
````

`that`은 고유 변수이므로 클로저가 접근할 수 있다.

- 조금 특이한 패턴

````javascript
(obj.getName)(); // Obj
(obj.getName = obj.getName)(); // Window
````

obj.getName에 할당한 값은 함수 자체이므로 this 값은 유지되지 않는다.

## 클로저는 어디서 사용되는가? 

- 클로저로 블록스코프 흉내내기

````javascript
(function() {
	// 코드
})();
````

`function(){}` 을 괄호로 감싸서 함수 표현식을 알리고 바로 실행한다.(안쓰면 에러가 난다)

````javascript
function outputNumbers(count) {
    (function() {
        for(var i=0; i<count; i++) {
            alert(i);
        }
    })();
  	alert(i); // 에러
}
````

위와 같은 패턴은 모듈화나, 공동작업시에 namespace로서 변수가 중복사용되지 않게끔 하는 용도로 많이 사용된다. 해당 스코프가 끝나면 메모리도 회수되기 때문에 메모리 효율도 좋다.

- private variable

````javascript
function myHome(thing) {    // 외부함수
  return { // 객체 리턴
    getThing : function() { // 내부함수
      return thing; // 외부함수의 지역변수를 사용할 수 있다.
    },
    setThing : function(_thing) {
      if(typeof _thing === 'String') {
        thing = _thing;
      } else {
        console.log('물건은 문자열이어야 합니다.');
      }
    }
  }
}
var notebook = myHome('Gram'); // notebook에 객체를 담음.
var tv = myHome('iptv');

console.log(notebook.getThing()); // Gram
console.log(tv.getThing()); // iptv

notebook.setThing('mac');
console.log(notebook.getThing()); // mac
````

notebook과 tv는 똑같은 객체(myHome의 리턴값)를 담고 있지만, 각 메서드들이 접근할 수 있는 thing(외부함수의 지역변수)의 값은 다름.

getThing/setThing은 public이지만, 내부적으로 사용하고 있는 thing은 외부함수의 지역변수로 이미 사라졌기 때문에 내부함수를 통해서만 접근할 수 있는 변수가 된다.

## Reference

https://www.inflearn.com/course/%EC%A7%80%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%96%B8%EC%96%B4-%EA%B8%B0%EB%B3%B8/%EB%82%B4%EB%B6%80%ED%95%A8%EC%88%98-%EC%99%B8%EB%B6%80%ED%95%A8%EC%88%98/