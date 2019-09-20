---
title: Bookshelf plugins를 살펴보자
date: 2018-12-22 19:28:10
categories:
    - Node.js
---

Bookshelf에 다양한 플러그인들이 많은데, 이번기회에 쓸만한 플러그인이 있나 한번 훝어 보기로 했다.

https://bookshelfjs.org/#plugins

### Virtuals

https://github.com/bookshelf/bookshelf/wiki/Plugin:-Virtuals

````javascript
const bs = require('bookshelf')(knex).plugin(['virtuals']);
var ModelWithVirtuals = bookshelf.Model.extend({
  virtuals: {
    fullName: function() {
        return this.get('firstName') + ' ' + this.get('lastName');
    }
  }
});
````

virtuals 안에 새로운 칼럼을 조작해서 만들 수 있다!

### Processor

https://github.com/bookshelf/bookshelf/wiki/Plugin:-Processor

같은 칼럼을 조작하고 싶을때! 인자로 함수를 넘겨야함.

````javascript
bookshelf.plugin('processor')

var castToDate = require('./processors/to-date')

var MyModel = bookshelf.Model.extend({
  tableName: 'things',
  processors: {
    // loginDate is a model attribute name
    loginDate: function(value) {
      return new Date(value);
    }
  }
})
````



### hidden

패스워드 같은 것을 리턴되지 않게 할 수 있음!

````javascript
const bs = require('bookshelf')(knex).plugin(['visibility']);
Db.Users = Orm.Model.extend({
  tableName: 'users'
, hidden: ['password', 'salt', 'secret', 'hashtype']
});

// toJSON() 할때 이런식으로 하면 해당 칼럼이 빠짐
toJSON({ visibility: false })
````



###  bookshelf-signals

https://github.com/bogus34/bookshelf-signals

이벤트를 각 모델에 셋팅할 필요 없이 중앙에다가 셋팅할 수 있음.

````javascript
const Signals = require('bookshelf-signals')
const db = require('bookshelf')(knex).plugin([Signals]);

class User extend db.Model({
  tabeName: 'users'  
})

db.on('saved', User, () => console.log('user was saved!'))
````

on(String event, [(Class|String) cls], Function handler)

두번째 인자가 배열인것에 주목!! 로깅을 위한 공통 createdAt 이나 updatedAt 같은것을 이곳에서 한꺼번에 셋팅할 수 있겠다.



https://bookshelfjs.org/#plugins

그외에도 더 많은 플러그인이 있으니 위 링크 참조



## Reference

https://bookshelfjs.org/#plugins

