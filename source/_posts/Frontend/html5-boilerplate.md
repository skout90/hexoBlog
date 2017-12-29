---
title: Html5 Boilerplate
date: 2017-10-08 19:28:10
categories:
    - Frontend
---

웹스톰 새프로젝트 만들다가 보았는데.

웹개발의 필수적인 요소만 모아둔 프로젝트인듯 하다.

> git clone https://github.com/h5bp/html5-boilerplate

**index.html**

- X-UA-COMPATIBLE, IE=edge : 호환성 보기 제거


- jquery loading fallback : CDN 사용 실패하면 나의 jquery 사용


- Google Analytics 비동기 로드 최적화

**main.css, normailze.css**

- HTML5 요소를 지원하지 않는 브라우저를 위한 표시 처리
- IOS 방향 변경시 텍스트 조정
- 모바일 사용자 줌기능 방지 처리
- 폼 요소 표시 최적화 

**modernizr**

- html5, css3의 기능을 사용할 수 있는지 여부 테스트. 결과를 html 태그의 클래스 이름으로 설정해주는 라이브러리

**etc**

- 웹 크롤러제어/flash용 크로스 도메인 정책/humans.txt

## Reference

https://github.com/h5bp/html5-boilerplate

https://www.slideshare.net/UyeongJu/html5-boilerplate-22608784