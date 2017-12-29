---
title: 외부 네트워크에서 내 PC로 접속 가능하게 하기
date: 2017-12-07 19:28:10
categories:
    - Etc
---

NAT와 PAT를 알아야 하는데

NAT(Network address translation)은  [사설 네트워크](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%84%A4_%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)에 속한 여러 개의 호스트가 하나의 공인 IP 주소를 사용하여 [인터넷](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7)에 접속하기 위함으로, 사설 IP를 라우터에서 공인 IP주소로 바꿔준다.

PAT(Port Address trasnlation)는 한 개의 공인 IP주소와 여러 개의 사설 IP 주소를 포트번호를 사용하여 물린다. 공유기가 바로 이 PAT를 사용한 통신이다.



**그래서 어떻게 외부 망에서 내 PC로 접속 가능하게 하냐면.**

공유기 설정에 들어가서, 공유기 포워딩 기능을 활용하여

외부에서 공인 IP의 특정 포트로 접속하는 경우, 나의 사설 IP로 포워딩 해준다!



이때 DDNS(Dynamic Domain Name Service)를 활용하여, 유동 IP에 네이밍을 부여해줄 수 있다.(iptime에서 지원한다고 함)

## Reference

우동사 쫑형

http://kentj.tistory.com/3