---
title: express session 정리
date: 2017-10-24 19:28:10
categories:
    - Node.js
---

express-session과 connect-session-knex를 이용하여 세션관리를 하였다.

```javascript
let session = require('express-session');
let KSS = require('connect-session-knex')(session);

app.use(session({
    //resave: true,
    secret: 'abcd',
    cookie: {secure: false, maxAge: null},
    store: new KSS({knex: knex, tablename: 'sessions'})
}));
```

#### session(options)

세션 미들웨어를 생성한다. 세션 데이터는 쿠키가 아닌 서버사이드에 저장된다.

> cookie-parser가 없어도 동작하지만, 만약 있다면 secret을 일치시키는 것이 좋다.

기본 서버 세션 저장소인 MemoryStore은 개발 환경을 위한 것.

<프로퍼티>

- cookie

  maxAge : 만료 시간을 밀리초 단위로 설정

  expires : 만료 날짜를 GMT 시간으로 설정(maxAge와 동시 등록시 마지막것 사용)

  path : cookie의 경로 default "/"

  domain : 지정한 도메인으로 쿠키값을 저장한다.

  secure : https에서만 cookie 사용할 수 있도록 한다.(HTTPS여야만 작동)

  httpOnly : 웹서버를 통해서만 cookie 접근할 수 있도록 한다

  signed : cookie가 서명되어야 할 지를 결정한다.

  sameSite : true/false 엄격하게 같은 사이트에서 쿠키를 사용할지.

- genid

지정된 함수로 세션아이디를 사용한다.

````javascript
app.use(session({
  genid: function(req) {
    return genuuid()
  },
  secret: 'keyboard cat'
}))
````



## Reference

