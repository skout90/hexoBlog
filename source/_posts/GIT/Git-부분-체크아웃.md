---
title: Git 부분 체크아웃(sparse checkout)
date: 2017-08-20 19:28:10
categories:
    - GIT
---

> $ mkdir [폴더이름]
>
> $ cd [폴더이름]
>
> $ git init
>
> $ git remote add -f origin [git url]
>
> $ git config core.sparseCheckout true

해당 폴더 .git/info에 sparse-checkout 파일 생성후, 체크아웃할 폴더이름을 적어준다.

> $ git pull origin master



## Reference

https://stackoverflow.com/questions/600079/how-do-i-clone-a-subdirectory-only-of-a-git-repository/13738951