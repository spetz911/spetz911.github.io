---
layout: post
title: ssh и http доступ к VirtualBox
date: 2012-06-07
comments: true
categories:
---

ssh и http доступ к VirtualBox при приспользовании NAT

1 comment so far

Настройка производится с помощью VBoxManage.

VBoxManage -- утилита командной строки, позволяющая вам контролировать

все возможности VirtualBox.

\

\<\<Особенность\>\> технологии NAT состоит в том, что гостевая и
хост-машина

никак не \<\<видят\>\> друг друга в IP-сети. Самое простое решение --
проброс

(форвард) портов средствами VirtualBox.

Настраиваем при выключенной гостевой машине.

Настраиваем доступ по ssh
``` bash
VBoxManage setextradata \<guestname\>
"VBoxInternal/Devices/e1000/0/LUN\#0/Config/ssh/HostPort" 2222
VBoxManage setextradata \<guestname\>
"VBoxInternal/Devices/e1000/0/LUN\#0/Config/ssh/GuestPort" 22
VBoxManage setextradata \<guestname\>
"VBoxInternal/Devices/e1000/0/LUN\#0/Config/ssh/Protocol" TCP
```
Доступ к http
``` bash
VBoxManage setextradata \<guestname\>

"VBoxInternal/Devices/e1000/0/LUN\#0/Config/guesthttp/Protocol" TCP

VBoxManage setextradata \<guestname\>

"VBoxInternal/Devices/e1000/0/LUN\#0/Config/guesthttp/GuestPort" 80

VBoxManage setextradata \<guestname\>

"VBoxInternal/Devices/e1000/0/LUN\#0/Config/guesthttp/HostPort" 8080
```

Запускаем машину

Проверяем ssh доступ
``` bash
ssh localhost -l  -p 2222
```
По http виртуальная машина доступна на 8080м порту
```
http://localhost:8080/
```
\<guestname\> -- имя виртуальной машины

\<username\> -- пользователь виртуальной машины

Comments
--------
