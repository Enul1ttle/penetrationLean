## Google的常用语法及其说明
```
site            #指定域名
inurl           #URL中存在的关键字的网页
intext          #网页正文中的关键字
intitle         #网页标题中关键字
filetype        #指定文件类型
link            #搜索一个网页的链接
info            #查找指定站点的一些基本信息
cache           #显示页面缓存
```
### 10个简单有效的搜索
```
site:baidu.com -www    #搜索子域名
intitle:index.of       #目录遍历
error | warning         #错误信息
login |logon           #后台
username | userid |employee.ID | "your username is"  #用户名
password |passcode |"your password is"  #密码
admin | administrator  #后台管理
-ext:html -ext:asp -ext:php #从搜索结果中除去常见的文件，有趣的信息就会浮出水面
inurl:temp inurl:tmp inurl:backup inurl:bak  #临时文件和备份
filetype:txt filetype:bak filetype:sql       #敏感文件
```
### 一些有趣的用法
```
inurl:nqt.php intitle:"Network Query Tool"  #搜索网络查询工具
filetype:txt  账号
site:cn  intext:后台管理
intitle:Password:  inurl:aspx  #密码重设页面
intitle:aspxshell filetype:aspx  #查找webshell
inurl:https://trello.com AND intext:@qq.com AND intext:password  #搜索trello.com 泄露的密码
inurl:https://trello.com AND intext:ssh AND intext:password
site:github.com AND intext:ftp AND intext:password
site:www.example.com asmx/xml
```
### 最后
- 谷歌黑客数据库：https://www.exploit-db.com/google-hacking-database
- 自动化工具：https://github.com/Smaash/snitch
### 补充
多使用几个搜索引擎，比如baidu,bing，毕竟每个搜索引擎收集到的可能会不一样。bing（国际版）对越权目录有奇效


