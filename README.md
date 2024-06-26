# Домашнее задание к занятию "`Уязвимости и атаки на информационные системы`" - `Сайфиев Денис`
---

### Задание 1
скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/ .

Это типичная ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину с помощью nmap .

пытаемся найти уязвимости, в которых происходит эта виртуальная машина.

Сами уязвимости можно найти на сайте https://www.exploit-db.com/ .

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

Какие сетевые службы в ней разрешены?
Какие уязвимости обнаружены вами? (список со ссылками: достаточно трёх уязвимостей)
Примите ответ в свободной форме.

### Решение 1

#### 1. Разрешенные сетевые службы
```
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login?
514/tcp  open  shell       Netkit rshd
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
```
 #### 2. Обнаруженные уязвимости
```
 17491
 15449
 16922
```
* https://www.exploit-db.com/exploits/17491
* https://www.exploit-db.com/exploits/15449
* https://www.exploit-db.com/exploits/16922



### Задание 2

Проведите диагностику Metasploitable в режимах SYN, FIN, Xmas, UDP.
Запишите сеансы в Wireshark.

Ответьте на следующие вопросы:

Как распределяются эти режимы с точками зрения сетевого трафика?
Как отвечает сервер?
Примите ответ в свободной форме.


### Решение 2

* SYN наиболее популярный вид сканирования. SYN/ASK - указывает на перечень открытых и прослушиваемых портов, SYN/RST - об обратном, а именно сбросе. Порт не прослушан и подвергается фильтрации.
```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sS 192.168.56.7
```

* FIN - Устанавливает только бит TCP FIN. Устанавливает соединение посредством системного вызова с последующим корректным закрытием соединения.

```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sF 192.168.56.7
```

* Xmas - в сканировании, при отправке пакетов на каждый запрос используются несколько доступных флагов для контроля соединения.
```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sX 192.168.56.7
```
  
* UDP - при данном виде сканирования на каждый порт отправляется "пустой" пакет. В зависимости от ответа определяется открытость или закрытость порта.
```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sU 192.168.56.7
```
