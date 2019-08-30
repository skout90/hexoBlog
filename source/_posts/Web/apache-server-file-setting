---
title: Apache(webtier) 서버 파일(nas) 웹서버를 통해 Response 하기
date: 2019-08-30 19:28:10
categories:
    - Web
---


웹티어(Webtier)는 아파치와 동일하게 설정을 가져간다고 한다
 
`httpd.conf` 파일을 수정하면 된다.
 
 - 웹티어 경로
 
/www/webtier/domains/[도메인주소]/config/fmwconfig/components/OHS/VCWeb1/httpd.conf
 
 > 못찾을 경우 find / -name "httpd.conf" 를 검색해서 알아내자!
 
### alias 설정


````
<IfModule alias_module>
   # ...

    Alias /vcomattach /vcomattach

````

> Alias /불러올 경로 /실제 파일 경로 



### 해당 디렉터리의 권한 설정

- httpd.conf

````
<Directory /path>
    AllowOverride none
    Require all granted
</Directory>
````

alias 설정과 권한 설정 모두 하위 디렉터리가 다 포함된다.

웹서버에 다음과 같이 접근 가능

`웹서버주소/alias에등록한 경로`
