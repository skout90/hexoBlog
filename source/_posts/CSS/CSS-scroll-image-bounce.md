---
title: scroll시 이미지 bounce 시키기
date: 2019-12-16 19:28:10
categories:
    - CSS
---

````html
<style>
  .container {
      position: absolute;
      top: 130px;
      left: 177px;
      z-index: 5;
  }
  .ani_margin_top {
      margin-top: -60px;
  }
  .ani_margin {
			padding-top: 60px;
  }
  .transition_ani1 {
      -webkit-transition: all 2.1s ease;
      -moz-transition: all 2.1s ease;
      -o-transition: all 2.1s ease;
      transition: all 2.1s ease;
      animation-timing-function: cubic-bezier(0,0,0.2,1);
      -webkit-animation-timing-function: cubic-bezier(0,0,0.2,1);
  }
</style>

 <div class="container transition_ani1 ani_margin ani_motion_2 ani_margin_top">
   <img src="assets/img/image.png">
</div>
````
