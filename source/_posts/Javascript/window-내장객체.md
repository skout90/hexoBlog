---
title: Window 내장객체
date: 2017-10-09 19:28:10
categories:
    - Javascript
---

#### 프로퍼티

#### length

창안의 프레임수

#### self/window



#### 메서드



## 이벤트

#### onload

문서를 읽을때, 실행된다.

#### onbeforeunload

브라우저 창을 닫거나, 다른 주소로 이동하면 실행되는 이벤트, *크롬에서는 보안상의 이유로 작동하지 않는다.*

````javascript
window.onbeforeunload = function(e) {
  var dialogText = 'Dialog text here';
  e.returnValue = dialogText;
  return dialogText;
};
````

#### onblur

브라우저가 포커스를 잃을 때 실행되는 이벤트, 탭 전환시, alt+tab 시에도 적용된다.

#### onfocus

브라우저가 포커스를 얻을때 실행되는 이벤트, 탭 전환시, alt+tab 시에도 적용된다.

## Reference

