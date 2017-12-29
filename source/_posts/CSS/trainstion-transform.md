---
title: transition, transform, animation - 박스 굴리기
date: 2017-10-09 19:28:10
categories:
    - CSS
---

````html
<style>
.box {
    border-style: solid;
    border-width: 1px;
    display: block;
    width: 100px;
    height: 100px;
    background-color: #0000FF;
    -webkit-transition:width 2s, height 2s, background-color 2s, -webkit-transform 2s;
    transition:width 2s, height 2s, background-color 2s, transform 2s;
}
.box:hover {
    background-color: #FFCCCC;
    width:200px;
    height:200px;
    -webkit-transform:rotate(180deg);
    transform:rotate(180deg);
}
</style>

    <p>아래 박스는 width, height, background-color, transform을 위한 트랜지션을 결합합니다. 박스 위에 마우스를 올려 속성들의 애니메이션을 보세요.</p>
    <div class="box"></div>
````

<style>
.box {
    border-style: solid;
    border-width: 1px;
    display: block;
    width: 100px;
    height: 100px;
    background-color: #0000FF;
    -webkit-transition:width 2s, height 2s, background-color 2s, -webkit-transform 2s;
    transition:width 2s, height 2s, background-color 2s, transform 2s;
}
.box:hover {
    background-color: #FFCCCC;
    width:200px;
    height:200px;
    -webkit-transform:rotate(180deg);
    transform:rotate(180deg);
}
</style>

    <p>아래 박스는 width, height, background-color, transform을 위한 트랜지션을 결합합니다. 박스 위에 마우스를 올려 속성들의 애니메이션을 보세요.</p>
    <div class="box"></div>

> block, inline-block 요소여야 하는 걸로 추정된다.

### transition

애니메이션을 실행할 시간을 지정할 수 있음.

`-webkit-transition:width 2s, height 2s, background-color 2s, -webkit-transform 2s;`

다음처럼, 높이/넓이, 배경색, 이동에 대한 transition 값을 지정해 주었음.

+ 추가적인 속성 정리 예정

### transform

객체를 움직인다.

```
transform: rotate(90deg); // 회전
transform: skewx(10deg) translatex(150px); // 비틀고 옮긴다.
transform-origin: bottom left; // 초기 위치
```

### animation

참고 : https://www.w3schools.com/css/tryit.asp?filename=trycss3_animation3

````css
@keyframes example {
    0%   {background-color:red; left:0px; top:0px;}
    25%  {background-color:yellow; left:200px; top:0px;}
    50%  {background-color:blue; left:200px; top:200px;}
    75%  {background-color:green; left:0px; top:200px;}
    100% {background-color:red; left:0px; top:200px;}
}

div {
    width: 100px;
    height: 100px;
    background-color: red;
    position: relative;
    -webkit-animation-name: example; /* Safari 4.0 - 8.0 */
    -webkit-animation-duration: 4s; /* Safari 4.0 - 8.0 */
    animation-name: example;
    animation-duration: 4s;
}
````



## Reference

https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions

https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Transforms/Using_CSS_transforms

