---
title: this 바인딩 분석
date: 2018-12-28 19:28:10
categories:
    - Javascript
---

## 기본 바인딩

전역함수 내에서 this 호출시 **this = window**

````javascript
function getFruitName() {
  console.log(this.name);
}

var name = 'apple';

getFruitName(); // "apple"
````

## 암시적 바인딩

### 객체 function 함수 할당시

객체 내에 function 함수를 호출시 **this = 해당 객체**

````javascript
function getFruitName() {
  console.log(this.name);
}

const obj = {
    name: 'apple',
    onPress: getFruitName
}

obj.onPress(); // "apple"
````

### 객체 arrow function 함수 할당시

객체 내 arrow function 함수 호출시 **this = 해당 컨텍스트의 부모 객체**

> arrow function은 의도적으로 컨텍스트를 할당할 수 있기 때문에 명시적 할당에 더 가깝다고 볼 수도 있다.

````javascript
var name = 'banana'
const z = {
    name: 'apple',
    onPress: () => console.log(this.name)
}
z.onPress(); // banana
````

### 객체에 할당된 function 함수를 복사시

````javascript
function getFruitName() {
  console.log(this.name);
}

var name = 'banana'

const obj = {
    name: 'apple',
    getFruitName: getFruitName
}

const getCopyFruitName = obj.getFruitName

getCopyFruitName() // banana
````

getCopyFruitName은 일반 함수이므로 obj.getFruitName을 할당하는 순간, this는 전역 객체가 되어버린다.

## 명시적 바인딩

우리가 의도한대로, this를 바인딩해보자!

````javascript
function getFruitName() {
  console.log(this.name);
}

var name = 'banana'

var obje = {
    name: 'apple',
    onPress: getFruitName
}

const getCopyFruitName = obje.onPress
const getCorectCopyFruitName = obje.onPress.bind(obje)

getCopyFruitName() // banana
getCorrectCopyFruitName() // apple
````



## Reference

http://enarastudent.tistory.com/entry/null과-undefined의-차이

https://stackoverflow.com/questions/1068834/object-comparison-in-javascript

