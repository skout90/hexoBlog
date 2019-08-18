---
title: React Native dev/Staging/Production 코드 푸시 적용 참고 링크
date: 2018-12-05 19:28:10
categories:
    - React
---



## 셋팅 방법

https://github.com/kjk7034/ReactNativeStudy/blob/master/docs/CodePush.md



## 명령어 모음

```
"code-push:test-a": "code-push release-react bGlam-Inc/bglam-b2c-app-android android",
"code-push:prod-a": "code-push release-react bGlam-Inc/bglam-b2c-app-android android -d Production",
"code-push:info-a": "code-push deployment ls bGlam-Inc/bglam-b2c-app-android -k",
"code-push:test-i": "code-push release-react bGlam-Inc/bglam-b2c-app-ios ios",
"code-push:prod-i": "code-push release-react bGlam-Inc/bglam-b2c-app-ios ios -d Production",
"code-push:info-i": "code-push deployment ls bGlam-Inc/bglam-b2c-app-ios -k"
```