---
title: media 태그
categories:
  - CSS
date: 2017-07-24 18:43:13
---
출력 장치의 여러 특징을 분기 처리하여 하나의 HTML 소스가 여러가지 뷰를 갖도록 구현하는 명세.

`@media only all and (조건문) {실행문}`

- **@media** : 미디어 쿼리가 시작됨을 선언.
- **only** : 미디어 쿼리를 지원하는 사용자만 쿼리 구문을 해석(default only)
  - 지원 브라우저 : ie9+, chrome 21+, firefox 3.5+, safari 4.0+, opera 9+
- **all** : 미디어 쿼리를 해석해야 할 대상 미디어를 선언.
  - all/ screen/ print 등이 있음.
- **and** 또는 **or(,)**
- **(조건문)** 
  - orientation : 가로모드/세로모드 판별 (orientation:portrait), (orientation:landscape)
  - width / height : (min-width:768px), (max-height:500px)
- **{실행문}** :  CSS 코드를 작성



## Reference

http://aboooks.tistory.com/365

http://naradesign.net/wp/2012/05/30/1823/