---
title: float로 레이아웃 만들기
date: 2017-09-06 19:28:10
categories:
    - CSS
---

float로 다음 레이아웃을 만들어봅시다.

![img](http://i.imgur.com/okipVgU.png)

````html
<style>
  *{
    box-sizing:border-box;
  }
  .container {
    width : 500px;
    border: 1px solid gray;
    margin: auto;
  }
  header{
    border-bottom:1px solid gray;
    text-align: center;
  }
  nav{
    float: left;
    width:150px;
    border-right:1px solid gray;
  }
  main{
    float: left;
    width:200px;
    padding:10px 22px 5px 4px;
    border-left:1px solid gray;
    border-right:1px solid gray;
    margin-left: -1px;
  }
  aside{
    float: left;
    padding:20px;
    width:150px;
    border-left:1px solid gray;
    margin-left: -1px;
  }
  footer{
    clear: both;
    border-top:1px solid gray;
    padding:20px;
    text-align: center;
  }
</style>

<div class="container">
  <header>
    <h1>헤더</h1>
  </header>
  <nav>
    <ul>
      <li>html</li>
      <li>css</li>
      <li>javascript</li>
    </ul>
  </nav>
  <main>
    Lorem ipsum dolor sit amet!
  </main>
  <aside>
    라젠카
  </aside>
  <footer>
    푸터푸터
  </footer>
</div>
````

### box-sizing:border-box;

원래 width를 border를 제외하고 계산하는데, 같이 계싼하게 하는 옵션.

### float

`float:left;`로 설정하면, 다음 요소가 옆으로 흐르듯이 겹친다.

겹치고 싶지 않을 때는 `clear: both;`를 사용.

### width 설정

float를 설정하면, 스크롤을 줄였을때 div가 내려오기 때문에, width를 설정하여, 내려오지 않게 한다.

### margin-left: -1px;

border가 겹칠 때는 margin 값을 조작하여 해결!

## Reference

https://www.inflearn.com/course/css-%EA%B8%B0%EB%B3%B8%EB%B6%80%ED%84%B0-%ED%99%9C%EC%9A%A9%EA%B9%8C%EC%A7%80/float-%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-holy-grail-%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83/