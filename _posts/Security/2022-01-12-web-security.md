---
title:  "웹보안[1. Centos기초세팅,웹구축]"

categories:
  - Security
tags:
  - [Security, 웹보안]

toc: true
toc_sticky: true

date: 2022-01-12
last_modified_at: 2022-01-12
---

## CentOS 싱글부트

1. 부팅후 선택화면에서 e 

2. rhgb quiet => rw init=/bin/bash

3. ctrl + x  

4. vi /etc/selinux/config <br><br>#SELINUX=enforcing<br>
SELINUX=disabled

5. passwd    ( 비번번경 ) 
6. exec /sbin/init

## 네트워크 설정

cd   /etc/sysconfig/network-scripts/<br>
ls -l    ===>   ifcfg-ens33 확인<br>
vi ifcfg-ens33<br>

>DEVICE=ens33<br>
 IPADDR=192.168.10.101<br>
 NETMASK=255.255.255.0<br>
 GATEWAY=192.168.10.2<br>
 DNS1=168.126.63.1<br>
 ONBOOT=yes<br>

service network restart<br>
ip addr<br>
ping 8.8.8.8 확인<br> 

## GUI환경 만들기
 
yum group list<br>
yum group list |grep -P "Tools|GNOME"<br>
yum groupinstall "Development Tools"  <<<< 개발자도구 <br>
yum groupinstall "GNOME Desktop"<br> 

cat /etc/inittab   <======  기본 부팅레벨 <br>

systemrunlevel  << 부팅레벨<br>

0   종료<br>
1   single<br>
2   TUI (NFS 미지원)<br>
3   TUI (NFS 지원 )  ****<br>
4   unuse<br>
5   x11  (그래픽환경 )<br>
6   재부팅 <br>
 

systemctl get-default<br>
multi-user.target  << TUI 환경 <br>

systemctl set-default graphical.target <br>
systemctl get-default<br>
graphical.target  출력확인<br>
init 6 <br>

## 웹서버 구축


- 준비 설치

  rpm -qa &#124;grep http
<!--
&#124; = |
-->

- 웹서버 

  yum install httpd* -y

- 서비스 실행

  systemctl  start httpd<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;or<br>
  service httpd start<br>

- 포트확인 

  netstat -lntup &#124;grep http   ( 80/tcp 포트 확인 )

- 방화벽 해제 

  firewall-cmd  --permanent --add-service http	[ 설정 ] <br>
  firewall-cmd  --reload			[ 적용 ] <br>
  firewall-cmd  --list-all			[ 확인 ] <br>


## putty 설정 

window -> appearance -> Change (Font)  => consolas 굵게 14pt<br>
session => HOSTNAME 192.168.10.101
saved session => 이름지정 => save 

==간지(색바꾸기) ==<br>

colours<br>
배경색  Background<br>
글자색  Foreground<br> 

## 홈페이지 만들기
웹서버  DocumentRoot <br>

-> /var/www/html

vi index.html 
```html
<html>
  <head>
    <meta charset="utf-8">
    <title>SEVAS_WEB</title>
  </head>
  <body>
    요기가 진짜 내용이예요<br><br>
    <marquee width=600 bgcolor="red">
      <font size=10 color=black>
        SEVAS_TEST페이지에 오신것을 환영합니다.
      </font>
    </marquee>
    <br>
    TEST
  </body>
</html>
```