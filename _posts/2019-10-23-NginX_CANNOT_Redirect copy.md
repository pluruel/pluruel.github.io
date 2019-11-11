---
layout: post
title:  "NginX 리다이렉트 명령이 듣지 않음"
date:   2019-10-23 13:50:10 +0900
categories: #ssh
---

# 사용 환경
 - Centos 7
 - nginx/1.16.1
 
# 에러 발생 상황
 - Nginx의 Redirect기능을 이용하여 80포트를 8080에서 작동하는 jenkins와 매핑 도중 기본 페이지만 노출

# 원인
 - Nginx Config에서 기본 페이지를 로드하는 부분이 있었음

### 사용한 nginx.conf
~~~
http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;
    #이 부분에서 기본 페이지를 가져오는 설정이 있다!!!!!!
    #include /etc/nginx/conf.d/*.conf;
    server {
        listen 80;
        location / {
                proxy_pass          http://127.0.0.1:8080;
        }
    }

}
~~~
 
# 해결법
1. include /etc/nginx/conf.d/*.conf;를 주석처리하고 새로 작성한다
2. /etc/nginx/conf.d/*.conf; 파일을 수정한다

