---
title: Node 모듈 cookieParser란 무엇인가
date: 2017-10-24 19:28:10
categories:
    - Node.js
---

요청된 쿠키를 쉽게 추출할 수 있도록 해주는 미들웨어.

request 객체에 cookies 속성이 부여된다.

````javascript
var express      = require('express')
var cookieParser = require('cookie-parser')
 
var app = express()
app.use(cookieParser())
 
app.get('/', function(req, res) {
  console.log('Cookies: ', req.cookies);
})
 
app.listen(8080)
````

아래와 같이 커맨드를 날리면 쿠키 값을 확인할 수 있다.

> $ curl http://127.0.0.1:8080 --cookie "Cho=Kim;Greet=Hello" 

- cookieParser(secret, options)

> secret : signed 시키는 암호키로 string/array 형태 가능
>
> options
>
> maxAge : 만료 시간을 밀리초 단위로 설정
>
> expires : 만료 날짜를 GMT 시간으로 설정
>
> path : cookie의 경로 default "/"
>
> domain : 도메인 네임 default "loaded"
>
> secure : https에서만 cookie 사용할 수 있도록 한다.
>
> httpOnly : 웹서버를 통해서만 cookie 접근할 수 있도록 한다
>
> signed : cookie가 서명되어야 할 지를 결정한다.

- res.cookie(쿠키명, 값, options)

response(브라우저)에 쿠키 생성

````javascript
res.cookie('hasVisited', '1', {
    maxAge: 60*60*1000,
    httpOnly: true,
    path:'/visitors'
});
````

- res.clearCookie(쿠키명, options)

쿠키 제거, 경로를 지정했다면 options에 해당 경로를 넘겨 삭제할 수 있다.

````javascript
res.clearCookie('hasVisited', {path: '/visitors'})
````

## Reference

https://www.npmjs.com/package/cookie-parser

http://cinema4dr12.tistory.com/838

http://nujabes403.blogspot.kr/2015/03/express-middleware-cookie-parser.html