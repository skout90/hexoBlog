---
title: NodeJs ORM을 위한 Bookshelf, Knex
date: 2017-08-15 19:28:10
categories:
    - Node.js
---

Node.Js 로 ORM 환경을 지원하기 위해, Knex와 Bookshelf를 활용해보자.

Knex는 쿼리 빌더를 위한 라이브러리이며, Bookshelf는 knex가 만든 쿼리를 DB에 날리기 위한 JS 라이브러리 이다.

#### 설치

> $ npm install knex --save
> $ npm install bookshelf --save
> // 아래와 같은 DB 엔진을 선택하여 설치
> $ npm install pg
> $ npm install mysql
> $ npm install mariasql
> $ npm install sqlite3

- 초기화

````javascript
var knex = require('knex')({
  client: 'mysql',
  connection: {
    host     : '127.0.0.1',
    user     : 'your_database_user',
    password : 'your_database_password',
    database : 'myapp_test',
    charset  : 'utf8'
  }
});

var bookshelf = require('bookshelf')(knex);

var User = bookshelf.Model.extend({
  tableName: 'users'
});
````

#### 쿼리 실행

````javascript
// new 없이 모델 초기화
let subscriber = User.forge();

// 방법 4가지
subscriber.query('where', 'other_id', '=', '5')
.fetch(). then((model)=> {});

subscriber.query({where: {other_id: '5'}, orWhere: {key: 'value'}})
.fetch(). then((model)=> {});

subscriber.query(function(qb) {
qb.where('other_person', 'LIKE', '%Demo').orWhere('other_id', '>', 10);})
.fetch(). then((model)=> {});

let qb = subscriber.query();
qb.where({id: 1}).select()
.then((resp)=>{});
````

#### 관계 정의

.belongsToMany, .hasMany 와 같이 관계를 정의해줄 수 있다.

````javascript
...
var User = bookshelf.Model.extend({
  tableName: 'users',
  posts: function() {
    return this.hasMany(Posts, 'userId');
  }
  tags: function() {
  	return this.belongsToMany(Tag, 'posts', 'userId', 'tagId')  
  }
  wallet : function() {
  	return this.hasOne(Wallets, 'userId');  
  }
});

var Posts = bookshelf.Model.extend({
  tableName: 'posts',
  tags: function() {
    return this.belongsToMany(Tag);
  }
});

var Wallets = booksehlf.Model.extend({
    tableName: 'wallets',
    user : function() {
        return this.belongsTo(Users, 'userId');
    }
})

var Tag = bookshelf.Model.extend({
  tableName: 'tags'
})
````

- **hasOne**

> return this.hasOne(Wallets, 'userId');  

1: 0..1 의 관계이다.  Wallets에서 `userId`로 질의를한다. 

> User.forge().fetch({withRelated: ['wallet']})
>
> SELECT * FROM wallets WHERE userId = '사용자ID';

- **hanMany**

> return this.hasMany(Posts, 'userId');

1:다 의 관계를 갖는다.  Posts에서 `userId`로 질의를 한다.

> User.forge().fetch({withRelated: ['posts']})
>
> SELECT * FROM posts WHERE  postId IN (userId들 ....)

- **belongsTo** 

> var Wallet = .. 생략
>
> return this.belongsTo(Users, 'userId');

Users테이블에서 Wallet의 userId로 질의를 한다. 0..1 : 1 의 관계를 가진다.

> Wallet.forge().fetch({withRelated: ['user']})
>
> SELECT * FROM users WHERE userId = '사용자';

- **belongsToMany**

> var User = ...
>
> return this.belongsToMany(Tag, 'posts', 'userId', 'tagId')  

posts의 userId와 tagId를 사용하여, User와 Tag를 조인한다.

조인할때 디폴트로 user의 id와 tag의 id를 사용한다.

다른 포린키로 조인하려면, 5,6번째인자로 user의 foreignKey/tag의 foreignKey를 쓴다.

## Reference

http://bookshelfjs.org/#Model-instance-has