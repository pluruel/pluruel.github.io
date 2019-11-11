---
layout: post
title:  "도커 최신버전 설치"
date:   2019-10-31 13:50:10 +0900
categories: #ssh
---

# 사용 환경
 - Centos 7

~~~
yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-selinux  docker-engine-selinux docker-engine



yum install -y yum-utils device-mapper-persistent-data lvm2

yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

yum install docker-ce


systemctl start docker

systemctl enable docker

systemctl status docker
~~~

출처: https://eventhorizon.tistory.com/47 [블록체인 프로그래밍]