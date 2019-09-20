---
title: Bounce 애니메이션
date: 2019-04-01 19:28:10
categories:
    - CSS
---

````css
    .bounce {
      border : 1px grey solid;
      animation: q-bounce 2s infinite;
    }

    @keyframes q-bounce {
      0%, 20%, 50%, 80%, 100% {
        transform: translateY(0)
      }

      40% {
        transform: translateY(-30px)
      }
      60% {
        transform: translateY(-15px)
      }
    }

````



````html
  <div class="bounce">
    안녕하세요!
  </div>
````

<a class="jsbin-embed" href="https://jsbin.com/waqokamali/embed?html,css,output">JS Bin on jsbin.com</a><script src="https://static.jsbin.com/js/embed.min.js?4.1.7"></script>

