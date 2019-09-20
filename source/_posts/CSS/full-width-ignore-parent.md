---
title: 부모에 상관없이 width 100% 주는 법
date: 2017-09-01 19:28:10
categories:
    - CSS
---

상위 요소의 넓이나 높이에 관계없이, **100vw는 브라우저 화면의 넓이**,

**100vh는 브라우저 화면의 높이**를 뜻함.

![img](https://i.imgur.com/66Sj1pd.png)

````html
<style>
  div {
    min-height: 40px;
    box-sizing: border-box;
  }
  #parent {
    width: 400px;
    border: 1px solid black;
    margin: 0 auto;
  }

  #something {
    border: 2px solid red;
  }

  #wide-div {
    width: 100vw;
    margin-left: calc(-50vw + 50%);
    border: 2px solid green;
  }
</style>
<div id="parent">
  <div id="something">Red</div>
  <div id="wide-div">Green</div>
  <div id="something-else">Other content, which is not behind Green as you can see.</div>
</div>
````

vw 는 IE9 이상 및 그 외 브라우저에서 지원해줌.

calc 함수를 써서, left를 화면의 0의 위치에서 시작하게끔 함. (IE8 이상)

## Reference

https://stackoverflow.com/questions/31391459/how-can-i-expand-a-child-div-to-100-screen-width-if-the-container-div-is-smalle