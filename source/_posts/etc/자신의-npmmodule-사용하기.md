---
title: 수정한 npm_module 사용하기
categories:
    - etc
date: 2017-09-22 19:28:10
---

맘에 드는 npm_module을 수정하고 사용하고 싶을때..

1. 해당 git repository를 fork 한다
2. 수정한다.
3. pacakge.json에 다음과 같이 등록

> npm install https://github.com/<username>/<repository>/tarball/master --save

/tarball 이라는것으로 해야 한다. 그래야 gz파일이라는 걸로 다운받아지면서 설치가 가능함.

내가 수정한 knex-logger

https://github.com/skout90/knex-logger

## Reference

https://stackoverflow.com/questions/13300137/how-to-edit-a-node-module-installed-via-npm