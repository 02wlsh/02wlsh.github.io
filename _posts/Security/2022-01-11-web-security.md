---
title:  "웹보안[0. 기본세팅 및 풋프린트]"

categories:
  - Security
tags:
  - [Security, 웹보안]

toc: true
toc_sticky: true

date: 2022-01-11
last_modified_at: 2022-01-11
---

## Kali 싱글부트

싱글부트 : 일종의 안전모드

1. 부팅후 선택 화면에서 영문 e 

2. ro quiet splash 를 찾으세요~

3. 해당부분을 rw init=/bin/bash  => ctrl + x 

4. passwd root  =>  비밀번호 입력후 successfully 

5. exec /sbin/init

## 네트워크 설정

vi /etc/network/interfaces

auto eth0<br>
iface eth0 inet static<br>
address 192.168.10.10<br>
netmask 255.255.255.0<br>
gateway 192.168.10.2<br>

service networking restart  <-  네트워크 항상 재시작!!