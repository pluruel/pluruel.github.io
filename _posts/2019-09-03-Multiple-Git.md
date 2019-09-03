---
layout: post
title:  "다중 Git 계정 설정(SSH)"
date:   2019-09-03 09:50:10 +0900
categories: #git
---

# SSH 생성/저장

다중 깃 접속의 골자는 SSH 접속이다.

Key 생성
~~~
    ssh-keygen -t rsa -b 4096 -C "email@email.com"
~~~

.ssh/config에 Key 등록

~~~
// 호스트명은 github.com-아이디
// 동일 계정은 동일 SSH접속이 가능 
// 계정이 다를 경우 새로운 키를 Generate 해야 함(위의 이메일을 바꾸어야 함.)
Host github.com-{gitid}
  HostName github.com
  User git
  IdentityFile ~\.ssh\generatedKey
~~~

# SSH 키 등록

Git -> Personal Setting -> SSH and GPG keys -> New SSH Key를 눌러 생성된 파일 중 .pub파일 내용을 복붙한다

# git config 파일 변경

SSH접근을 원하는 Git Repository 폴더/.git/config
~~~
[remote "origin"]
url = {Host}:{ID}/{REPO_NAME}.git
fetch = +refs/heads/*:refs/remotes/origin/*
~~~
Git repo 에서 clone or download 버튼을 누르면 ssh 주소가 나오고 
{Host}위치를 수정하면 된다.이는 위의 .ssh/config 에서 수정한 Host의 이름과 같게 하면 끝.

다음을 입력하여 확인
~~~
ssh -T git@github.com
~~~