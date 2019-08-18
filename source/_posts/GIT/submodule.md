---
title: 서브모듈 추가하기
date: 2018-01-07 19:28:10
categories:
    - Vue
---

1. 서브모듈 추가

> git submodule add 주소

2. 서브모듈 로그 확인

> cd 서브모듈
>
> git log --pretty=short -1

3. 서브모듈 pull

> cd 서브모듈
>
> git pull origin master

서브모듈의 revision 정보를 더함.

> git add 서브모듈





서브 모듈 프로젝트 클론

> git clone 부모프로젝트
>
> cd 부모프로젝트
>
> git submodule init
>
> git submodule update



- 웹스톰 파일 수정이 안될때

> sudo chown -R 유저이름 서브모듈폴더

## Reference

Vue.js Quick Start 원형섭