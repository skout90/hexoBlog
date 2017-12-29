---
title: Webstorm 에서 NodeJs Express 디버깅하기
date: 2017-08-20 19:28:10
categories:
    - Node.js
---

삽질 끝에 디버깅하는데 성공했다.. 방법을 공유한다.

> 환경 : window 7, node express, nodemon

nodemon을 통해 자동으로 서버를 재 실행되게 하는데, nodemon을 사용하지 않으면 더 간편하게 디버깅이 가능하다.

#### nodemon을 사용할 경우

nodemon을 사용할 경우에만 아래작업을 한다. 그렇지 않을 경우는 생략한다.

  1. 메뉴 -> Run -> Edit Configurations
  2.  \+ 버튼을 눌러 Node.js Remote Debug 을 생성한다.
  3. port를 번호를 기억한다.

![img](http://i.imgur.com/DNgzV16.png)

#### 디버깅 설정

1. \+ 버튼을 눌러 Node.js를 생성한다.
2. Node interpreter에 node.exe의 경로를 셋팅한다
3. Node parameters에 nodemon의 경로를 넣는다. 
4. (nodemon 사용할 시에만) Node parameters 뒤에 `--debug=위에서 기억한 포트` 를 입력한다.
5. Javascript file : 에 express 서버 실행 파일 `www` 파일을 입력한다.

![img](http://i.imgur.com/uxW5JLW.png)

#### 디버깅 시작

우선 위에서 등록한 node.js 와 remote 중에 node.js 를 `Run` 으로 실행한다. 그 후, remote를 `Debug`로 실행한다. 브레이킹 포인트를 찍으면 되는 모습을 확인할 수 있다!



## Reference

https://vcfvct.wordpress.com/2015/02/13/debug-nodejs-with-nodemon-and-intellij/