---
title: Lets Encrypt활용 nginx에서 5분만에 https 설정하기
date: 2018-09-01 19:28:10
categories:
    - Web
---

nginx와 certbot을 이용하면 https 적용이 너무 쉽다...... 괘난 삽질을 많이 한듯.

> 환경 ubuntu 16.0.4

- nginx 설치

> sudo apt install nginx
>
> sudo service nginx start

- nginx 경로로 이동

> cd /etc/nginx/conf.d
>
> sudo vi servers.conf

- 서버 정보 입력

````shell
server {
    listen  80;
        server_name     [도메인 주소 입력];
        location / {
        proxy_pass      http://localhost:[포트];
        proxy_set_header        Host    $host;
        proxy_set_header        X-Real-IP       $remote_addr;
        proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_connect_timeout   150;
        proxy_send_timeout      100;
        proxy_read_timeout      100;
        proxy_buffers   4 256k;
        proxy_buffer_size       128k;
        proxy_busy_buffers_size 256k;
        client_max_body_size    8m;
        client_body_buffer_size 128k;
    }
}

````

- nginx 재시작

> ```
> $ sudo nginx -t
> $ sudo service nginx reload
> ```

- certbot 설치

> sudo add-apt repository ppa:certbot/certbot
>
> sudo apt-get update
>
> sudo apt-get install certbot



- certbot nginx plugin 통해 SSL 인증이 자동으로된다!!

> cd certbot
>
> certbot-auto -\-nginx -d example.com -d www.example.com
>
> 

그럼 아래와 같은 문구가 나옴

````shell
Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
-------------------------------------------------------------------------------
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
-------------------------------------------------------------------------------
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 2
````

여기서 2번을 선택하면, nginx 설정에 자동으로 https로 리다이렉트 해주는 명령어가 추가된다.

키도 자동으로 생성해준다!! 대단하지 않은가!!

- 테스트

<https://www.ssllabs.com/ssltest/>



적용 끝이다 놀랍지 않은가.

nginx plugin을 활용하지 않고, 직접 적용하려면 아래와 같이 하면 된다.

https://itnext.io/node-express-letsencrypt-generate-a-free-ssl-certificate-and-run-an-https-server-in-5-minutes-a730fbe528ca



## 갱신

매달 자동 갱신을 시키는 로직을 추가하자!

ubuntu 기준 스케줄러에 등록

> crontab -e

눌러 크론탭 수정화면 진입

>  0 4 1 * * /home/ubuntu/https/certbot/certbot-auto renew -\-q -\-no-self-upgrade

매달, 1일 4시 0분에 갱신 명령어 입력 저장후

> crontab -l

저장된 크론탭을 확인!

1개월마다 자동 갱신된다.

## Reference

https://twpower.github.io/44-set-free-https-by-using-letsencrypt

크론 사용 팁 : https://jdm.kr/blog/2

자동갱신 : http://riseshia.github.io/2016/10/16/certbot-let-s-encrypt.html