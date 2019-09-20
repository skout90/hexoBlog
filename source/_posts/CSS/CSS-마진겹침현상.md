---
title: CSS 마진 겹침 현상
date: 2017-09-03 19:28:10
categories:
    - CSS
---

## 마진겹침현상 세 가지

1. 위,아래 엘리먼트들의 마진이 겹칠시 둘 중 마진이 큰게 둘 사이의 마진이 된다.

````html
<style>
	div { border : 1px solid grey }
	.up { margin-bottom: 40px }
	.down { margin-top: 30px }
</style> 

<div class="up">abc</div>
<div class="down">def</div>
````

![img](http://i.imgur.com/Rz5XDXc.png)

2. 위,아래 엘리먼트들의 마진이 겹치고, 위의 엘리먼트의 시각적 요소가 없어지면, 시각적 요소가 없어진 엘리먼트 마진의 top-bottom과/ left-right은 큰값으로 합쳐져 계산된다.

````html
<style>
.up {
  margin-top: 30px;
  margin-bottom: 40px;
}
.down {
  border : 1px solid grey;
  margin-top: 20px;
}
</style>
  <div class="up"></div>
  <div class="down">def</div>
````

up의 margin-top/margin-bottom, down의 margin-top 중 가장 큰값으로 마진을 계산

3. 부모,자식 엘리먼트 사이에서 부모의 시각적 요소가 없어지면 부모,자식 마진 중 마진이 큰 쪽이 자식 마진처럼 사용된다.

````html
<style>
.parent {
  margin-top: 60px;
}
.child {
  border : 1px solid grey;
  margin-top: 30px;
}
</style>
<div class="parent">
  <div class="child">
  </div>
</div>
````

.child의 margin-top이 60 이상이 될때 적용된다. 그전에 겹쳐서 .parent의 margin-top 이 사용.

## Reference

생활코딩 CSS