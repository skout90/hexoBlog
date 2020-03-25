---
title: Facebook Pixel Code와 FB App Event의 차이점
categories:
  - etc
date: 2019-12-17 19:28:10
---

하이브리드 앱에서 페이스북 픽셀 “이벤트”는 웹에서 JS를 통해 동작함.

반면 FB App Event의 경우 네이티브 앱을 위해 만들어 졌음

따라서 하이브리드 앱에서 "앱 이벤트"를 사용할 경우, 아래와 같은 장점이 있다고 함.

- 앱 설치 이벤트 활용 가능

- 어플리케이션 버전, 디바이스 모델과 같은 구체적인 컨텍스트 정보 획득 가능

- 안정적 이벤트 로그 전송 가능

(https://developers.facebook.com/ads/blog/post/v2/2018/07/31/hybrid-web-apps)

픽셀 이벤트를 앱 이벤트로 인터셉트 하는 방법이 나와있음.
https://developers.facebook.com/docs/app-events/hybrid-app-events
