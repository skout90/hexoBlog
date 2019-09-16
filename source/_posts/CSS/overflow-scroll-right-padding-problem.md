---
title: overflow scroll 일시 right margin이 안먹는 문제
date: 2019-09-16 19:28:10
categories:
    - CSS
---

margin은 엘리먼트의 위치를 조정할뿐 wrapper의 크기를 확장시켜주지 않는다. 그래서 overflow: scroll일때 margin 값이 먹지 않는다.

다음과 같은 슈도 코드를 이용해서 해결할 수 있다.

```css
.wrapper {
    display: flex;
    flex-wrap: nowrap;
    overflow-x: auto;
    overflow-y: hidden;
    border: 1px grey solid;
}

.item {
    width: 200px;
    position: relative;
    margin-right: 20px;
    border: 1px red solid;
    flex-shrink: 0;
}


.item:last-child:after {
    content: "";
    display: block;
    position: absolute;
    right: -20px;
    width: 20px;
    height: 20px;
}
```

```html
<div class="wrapper">
    <div class="item">안녕</div>
    <div class="item">안녕</div>
    <div class="item">안녕</div>
    <div class="item">안녕</div>
    <div class="item">안녕</div>
    <div class="item">안녕</div>
    <div class="item">안녕</div>
    <div class="item">안녕</div>
</div>
```

<script async src="//jsfiddle.net/skout90/tupcyvsL/1/embed/"></script>

## Reference

https://blog.alexandergottlieb.com/overflow-scroll-and-the-right-padding-problem-a-css-only-solution-6d442915b3f4
