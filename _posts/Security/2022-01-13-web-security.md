---
title:  "웹보안[2. php설치 및 프록시 설정]"

categories:
  - Security
tags:
  - [Security, 웹보안]

toc: true
toc_sticky: true

date: 2022-01-13
last_modified_at: 2022-01-13
---

## php 설치

cd /var/www/html
vi index.php  ( WEB_TEST)

페이지가 안뜬다.


# 패키지 확인
rpm -qa |grep php 

php가 출력 안될경우 패키지를 설치해야함 
yum install -y php-*

* 에러메세지<br>
    php-mysql conflicts with php-mysqlnd-5.4.16-48.el7.x86_64 You could try using --skip-broken to work around the problem

yum install php-* 를 하게되면 충돌이 일어난다.<br>
yum install php-* --skip-broken으로 해결해준다.<br>

설치후 service httpd restart 후 페이지 확인