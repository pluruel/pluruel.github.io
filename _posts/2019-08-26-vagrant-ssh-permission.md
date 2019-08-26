---
layout: post
title:  "js"
date:   2019-08-26 16:50:10 +0900
categories: #js
---
# Vagrant 기반 가상 머신을 외부에서 접속하기

vagrant기반으로는 기본적으로 외부에서 ssh 접속을 할 수 없다. 
~~~ruby
config.vm.network :forwarded_port, guest: 22, host: 2222, host_ip: "0.0.0.0", id: "ssh", auto_correct: true
~~~
을 추가해 주면 외부에서도 ssh를 이용하여 접속할 수 있다.

# 해당 명령어를 사용하였는 데도 제대로 되지 않는 경우

이 경우 key 파일의 permission이 문제. 위의 명령어를 vagrantfile에 정상적으로 입력하였다면, key File의 사용 범위를 600정도로 지정해 주면 된다
