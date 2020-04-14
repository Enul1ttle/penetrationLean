## 信息收集
公司和个人网站是信息的重要来源，查看公司的LinkedIn个人资料，以确定高级经理，董事和非技术人员。 很多时候，最薄弱的密码属于许多公司的管理人员。 搜索公司网站上的“关于我们”页面也可以找到薄弱的目标。
```
IP地址段     
域名信息      
邮箱         
文档图片数据   
公司组织架构    
联系电话传真     
人员姓名/职务等信息
目标系统使用的技术
公开的商业信息
```
### whois
```
https://wq.apnic.net/static/search.html 
http://littlegreenfootballs.com/nqt.php?target=148.163.164.12  #这个能查edu这种域名
http://whois.chinaz.com/reverse  #反差邮箱  
https://www.reversewhois.io #反查邮箱，如果目标有邮服。比如@baidu.com 效果不错
https://domaineye.com/ #反差邮箱注册人
```
### 子域名采集
不要嫌麻烦，每个方法都要试一遍。可能试完所有的方法也就比爆破的多一两个，但那多出来的子域名很大可能就是突破口。
```
- 域传送漏洞 
`nmap --script dns-zone-transfer --script-args dns-zone-transfer.domain=http://test.com -p 53 -Pn 192.168.5.6`
- 暴力猜解（常见域名字典、根据企业特点对字典做变形、循环遍历多级域名）
https://phpinfo.me/domain/                     #在线爆破
https://subdomainfinder.c99.nl                 #在线查找
https://github.com/lijiejie/subDomainsBrute    #子域名爆破
https://github.com/p1g3/JSINFO-SCAN            #爬取js采集子域名
https://github.com/aboul3la/Sublist3r          #子域名采集
https://github.com/Screetsec/Sudomy            #这个集合各大开源平台，省时省力
https://github.com/devanshbatham/ArchiveFuzz   #从 Web archiving 收集子域名，邮箱
http://dns.bufferover.run/dns?q=baidu.com      #opendata.rapid7 
- SSL证书信息 https://censys.io/certificates?q=baidu.com
- 搜索引擎（结合site语法，同时利用google的-、百度的-intitle等语法减少干扰）
- 对已知ip的域名反查
https://passivedns.mnemonic.no/ 
http://reverseip.domaintools.com/
http://serversniff.net.ipaddress.com/
https://www.robtex.com/
- 一些公开查询平台(如：dnsdumpster.com)
https://securitytrails.com/
https://x.threatbook.cn
- 有APP用MobSF反编译 
```
### 确定ip段
```
- whois 子域名的ip，大型目标能看到ip段
- spf 解析记录
http://www.kloth.net/services/nslookup.php
- vpn/邮服 附近的最有可能真实ip段
- `intext:@baidu.com IP  Reverse DNS  IP-range` 查看反向解析结果
- 用shodan，fofa,censys 等搜索目标域名和公司名称。
有些服务器维护人员喜欢打上自己的标签，例如特殊的HTTP头。 我们可以通过shodan或钟馗之眼 来进行搜索拥有同样标签的服务器。
- ip比较法
比较大型的目标会有比较多IP地址，大型目标网络ip地址通常分配在一个C段或多个c段中。
例目标顶级域名为www.seclines.com 其IP地址为222.222.222.222 ，bbs.seclines.com 其ip为222.222.222.223 wiki.seclines.con 其ip为222.222.222.224由此可以推测222.222.222.1-255的IP地址都为该公司IP地址，但最后的确定还要根据其他的信息进行判断。
```
### C段旁站
```
- C段信息
https://censys.io/ipv4?q=163.177.151.110/24
`site:163.177.151.*`
- 旁站
bing国际版：`ip:163.177.151.110`
- ip反查域名
https://passivedns.mnemonic.no/
https://www.virustotal.com/gui/ip-address/
https://tools.ipip.net/ipdomain.php
https://www.ip-address.org/reverse-lookup/reverse-ip.php
https://fofa.so/result?q=148.163.164.12
`intext:148.163.164.12 Reverse domain`
```

### 邮箱采集
```
- 可枚举漏洞
`nmap -p 25 --script smtp-enum-users.nse 202.38.193.203–script-args userdb=/root/user.txt,passdb=/root/password.txt`
- whois高级搜索
`
whois -h whois.arin.net "e @ icann.org" | grep -E -o "\b[a-zA-Z0-9.-]+@[a-zA-Z0–9.-]+\.[a-zA-Z0–9.-]+\b" | uniq
`
- 工具采集
https://github.com/m4ll0k/Infoga
https://github.com/laramies/theHarvester
- 社工裤泄露
https://pwndb2am4tzkvold.onion.ws/ #洋葱网络
- SSL证书信息 
SSL / TLS证书通常包含域名，子域名和电子邮件地址。这使他们成为攻击者的宝库。
https://censys.io/certificates?q=baidu.com
```
###  Google hacking
```
- 敏感信息泄露
site:github.com intext:baidu.com
site:pastebin.com  AND intext:baidu.com
site:searchcode.com  AND intext:baidu.com
site:trello.com.com  AND intext:baidu.com
- 网站历史数据爬取
https://github.com/devanshbatham/ArchiveFuzz  
https://github.com/melbadry9/WaybackUrls
https://github.com/si9int/cc.py
- 目录遍历
site:baidu.com intitle:index.of
parent directory site:www.example.com
- 后台查找
site:baidu.com intext:管理|后台|登陆|用户名|密码|验证码|系统|帐号|manage|admin|login|system|登入|logon | administrator AND inurl:login|admin|manage|manager|admin_login|login_admin|system
- 敏感文件
使用工具：https://github.com/Smaash/snitch
inurl:temp | inurl:tmp | inurl:backup| inurl:bak
filetype:txt | filetype:bak | filetype:sql |filetype:rar |filetype:doc
- 报错信息
error | warning |SQL syntax | MySQL Query fail
- 查找工具
inurl:nqt.php intitle:"Network Query Tool"
```
### Nmap
```
- 路由跟踪 
nmap --traceroute {ip}  #目标配置不当能看到内网ip
- 服务器信息
nmap -O -sV -sF -T4 {ip}
- 弱点扫描
漏洞脚本升级：`nmap --script-updatedb`
弱口令探测：`nmap --script=auth {ip}`
暴力破解：`nmap --script=brute {ip}`
扫描常见漏洞：`nmap --script=vuln {ip}` 
webdav远程执行漏洞扫描：`nmap --script=http-iis-webdav-vuln {ip}`
IIS<7.5 尝试短文件漏洞目录文件扫描：`nmap -p80 --script=http-iis-short-name-brute {ip}` 
显示http的title信息，便于发现重要系统：`nmap --script=http-title  {ip}` 
心脏滴血漏洞：`nmap --script=ssl-heartbleed {ip} -p443 http-put`
- 增强扩展
https://github.com/vulnersCom/nmap-vulners
- 常见端口信息及渗透
端口号       端口服务/协议简要说明           关于端口可能的一些渗透用途
tcp 20,21    ftp 默认的数据和命令传输端口[可明文亦可加密传输]  允许匿名的上传下载,爆破,嗅探,win提权,远程执行(proftpd 1.3.5),各类后门(proftpd,vsftp 2.3.4)
tcp 22    ssh[数据ssl加密传输]    可根据已搜集到的信息尝试爆破,v1版本可中间人,ssh隧道及内网代理转发,文件传输,等等…常用于linux远程管理…
tcp 23    telnet[明文传输]    爆破,嗅探,一般常用于路由,交换登陆,可尝试弱口令,也许会有意想不到的收获
tcp 25    smtp[简单邮件传输协议,多数linux发行版可能会默认开启此服务]    邮件伪造,vrfy/expn 查询邮件用户信息,可使用smtp-user-enum工具来自动跑
tcp/udp 53    dns[域名解析]    允许区域传送,dns劫持,缓存投毒,欺骗以及各种基于dns隧道的远控
tcp/udp 69    tftp[简单文件传输协议,无认证]    尝试下载目标及其的各类重要配置文件
tcp 80-89,443,8440-8450,8080-8089    web[各种常用的web服务端口]    各种常用web服务端口,可尝试经典的top n,vpn,owa,webmail,目标oa,各类java控制台,各类服务器web管理面板,各类web中间件漏洞利用,各类web框架漏洞利用等等……
tcp 110    [邮局协议,可明文可密文]    可尝试爆破,嗅探
tcp 137,139,445    samba[smb实现windows和linux间文件共享,明文]    可尝试爆破以及smb自身的各种远程执行类漏洞利用,如,ms08-067,ms17-010,嗅探等……
tcp 143    imap[可明文可密文]    可尝试爆破
udp 161    snmp[明文]    爆破默认团队字符串,搜集目标内网信息
tcp 389    ldap[轻量级目录访问协议]    ldap注入,允许匿名访问,弱口令
tcp 512,513,514    linux rexec    可爆破,rlogin登陆
tcp 873    rsync备份服务    匿名访问,文件上传
tcp 1194    openvpn    想办法钓vpn账号,进内网
tcp 1352    Lotus domino邮件服务    弱口令,信息泄漏,爆破
tcp 1433    mssql数据库    注入,提权,sa弱口令,爆破
tcp 1521    oracle数据库    tns爆破,注入,弹shell…
tcp 1500    ispmanager 主机控制面板    弱口令
tcp 1025,111,2049    nfs    权限配置不当
tcp 1723    pptp    爆破,想办法钓vpn账号,进内网
tcp 2082,2083    cpanel主机管理面板登录    弱口令
tcp 2181    zookeeper    未授权访问
tcp 2601,2604    zebra路由    默认密码zerbra
tcp 3128    squid代理服务    弱口令
tcp 3312,3311    kangle主机管理登录    弱口令
tcp 3306    mysql数据库    注入,提权,爆破
tcp 3389    windows rdp远程桌面    shift后门[需要03以下的系统],爆破,ms12-020[蓝屏exp]
tcp 4848    glassfish控制台    弱口令
tcp 4899    radmin远程桌面管理工具,现在已经非常非常少了    抓密码拓展机器
tcp 5000    sybase/DB2数据库    爆破,注入
tcp 5432    postgresql数据库    爆破,注入,弱口令
tcp 5632    pcanywhere远程桌面管理工具    抓密码,代码执行,已经快退出历史舞台了
tcp 5900,5901,5902    vnc远程桌面管理工具    弱口令爆破,如果信息搜集不到位,成功几率很小
tcp 5984    CouchDB    未授权导致的任意指令执行
tcp 6379    redis未授权    可尝试未授权访问,弱口令爆破
tcp 7001,7002    weblogic控制台    java反序列化,弱口令
tcp 7778    kloxo    主机面板登录
tcp 8000    Ajenti主机控制面板    弱口令
tcp 8443    plesk主机控制面板    弱口令
tcp 8069    zabbix    远程执行,sql注入
tcp 8080-8089    Jenkins,jboss    反序列化,控制台弱口令
tcp 9080-9081,9090    websphere控制台    java反序列化/弱口令
tcp 9200,9300    elasticsearch    远程执行
tcp 10000    webmin linux主机web控制面板入口    弱口令
tcp 11211    memcached    未授权访问
tcp 27017,27018    mongodb    爆破,未授权访问
tcp 3690    svn服务    svn泄露,未授权访问
tcp 50000    SAP Management Console    远程执行
tcp 50070,50030    hadoop    默认端口未授权访问
```
### web指纹
```
- 在线
https://www.whatweb.net/
https://builtwith.com/
https://whatcms.org/
http://www.yunsee.cn/
https://www.netcraft.com/
- 工具
https://github.com/TideSec/TideFinger    #整合多个指纹库
https://github.com/7z1/waf_identify      #整合四款waf识别工具
https://github.com/Tuhinshubhra/CMSeeK #CMS检测
- 浏览器
Firebug->Net查看HTTP响应头部Server字段
指定路径下指定名称的js文件或代码。
指定路径下指定名称的css文件或代码。
<title>中的内容，有些程序标题中会带有程序标识，但不是很多。
meta标记中带程序标识<meta name="description"/><meta name="keywords"/><meta name="generator"/><meta name="author"/><meta name="copyright"/>中带程序标识。
Wordpress  | <meta name="generator" content="WordPre 3.9.2"
phpBB      | <body id="phpbb"
Mediawiki  | <meta name="generator" content="Media Wiki 1.21.9"
Joomla     | <meta name="generator" content="Joomla!-Open Source Content Management"
Drupal     | <meta name="Genertor" content="Drupal 7"/>
DotNetNuke | DNN Platfrom -http://www.dnnsoftware.com
display:none中的版权信息。
页面底部版权信息，关键字? Powered by等。
readme.txt、License.txt、help.txt等文件。
指定路径下指定图片文件，如一些小的图标文件，后台登录页面中的图标文件等，一般管理员不会修改它们。
注释掉的html代码中<!--
http头的X-Powered-By中的值，有的应用程序框架会在此值输出。
robots.txt文件中的关键字
404页面
302返回时的旗标
cookie中的关键字
phpBB       | phpbb3_
Wordpress   | wp-settings
1C-Bitrix   | BITRIX_
AMPcms      | AMP
Django CMS  | django
DotNetNuke  | DotNetNukeAnonymous
e107        | e107_ez
EPiServer   | EPiTrace,EPiServer
GraffitiCMS | graffitibot
Hotaru CMS  | hotaru_mobile
ImpressCMS  | ICMSession
Indico      | MAKACSESSION
InstantCMS  | InstantCMS[logdate]
KenticoCMS  | CMSPreferrdCulture
MODx        | SN4[12symb]
TYPO3       | fe_type_user
Dynamicweb  | Dynamicweb
LEPTON      | lep[some_numeric_value]+sessionid
Wix         | Domain=.wix.com
VIVVO       | vivvoSessionId
```
### 公开漏洞搜索
```
exp搜索：https://sploitus.com/
cve详情：https://www.cvedetails.com/
https://www.exploit-db.com/papers
乌云镜像：http://www.anquan.us
台湾漏洞提交平台：https://zeroday.hitcon.org/vulnerability/disclosed
路由器漏洞：http://www.routerpwn.com/
默认密码：https://cirt.net/passwords
```
### web传统漏洞查找
```
- Fuzz 字典
https://github.com/danielmiessler/SecLists
https://github.com/Stardustsky/SaiDict
https://github.com/TheKingOfDuck/fuzzDicts
https://github.com/swisskyrepo/PayloadsAllTheThings
https://github.com/Enul1ttle/myfuzz
- 备份扫描
https://github.com/tismayil/ohmybackup
- 目录爆破
https://github.com/maurosoria/dirsearch  
- Burpsuit 插件
Autorize  越权
Wsdler  测试WSDL请求

- waf探测
https://github.com/7z1/waf_identify
- 是否负载均衡
`lbd www.baidu.com`
- 弱点扫描
Openvas，Nessus
 - web 漏扫
*Nikto*扫描内容：软件版本 、敏感文件 、配置问题 、xss、sql 、运气好能爆出网站的内网IP。
*Arachni*  特点：web界面直观 、多功能 、高性能的Ruby框架。
*XSStrike*  特点：反射型和DOM XSS扫描、多线程抓取 、可配置的核心、WAF检测和绕过
*Burpsuite* 2.0版本以上加强了漏洞扫描组件。
*sqlmap*  sql注入检测利用的神器。
```
#### F12信息收集
```
- 注释信息收集
【Ctrl+shift+f】搜索`<!--`
- hidden信息收集
有些参数虽然是hidden的，但依旧会提交到服务器
- 相对路径搜索
火狐浏览器右键`view image info`查看网页图片的相关信息，有些目录编辑器上传点放在后台目录后面。
- JS敏感信息泄露
`Firebug->Script`登陆框的js会着找到很多意外收获，可能某些链接存在未授权访。某次查看js文件，发现post userid=xxxx&weixinlog=1就能绕过密码登陆。还是使用范围很广的缴费系统。
- Network模块信息收集
查看http返回包，有时候能看到中间件的版本，webserver信息对于渗透来说是很重要的，通过获取的版本即可查找对应的漏洞进行利用，从而提高渗透的效率！查看cookie,如果你发现cookie中含有admin=0,或者flag=0的这类标志，你就可以使用burpsuit进行抓包进行截断改包，将0改为1可能就可以直接进入到系统中了。个人觉得只要是不常见的cookie标志，或者任何能输入的地方都可以使用Burpsuit Fuzzing试试。
- 细心很重要，当工具都识别不出事什么cms的时候，某次我看到x-ux.admin.css,就去百度搜，果然是一个基于thinkphp3.2.8开发的后台框架，刚想代码审计，就发现他直接用了百度WebUploader未授权上传的插件。
```
#### 浏览网页
```
- 注意公告栏，通知等信息。
- 根据发布的内容对命名模式推断 例如：发现一个viewuser.asp页面，然后就可以查找类似edituser.asp、adduser.asp和deleteuser.asp。如果/app/user目录被发现接着可以查找/app/admin 、/app/manager。
- 随手在网页后面加old、\~、bak、copy、orig 如config.asp.old。如果是网站是iis7.5，尝试config.asp/.php 运气好能读取到源码(iis7.5解析漏洞)。
- 利用User Agent Switcher切换不同的User Agent然后访问同一个特定页面。这是因为很多的Web应用对于不同的User-Agent和Referer请求头会返回不同的内容。
```
#### 杂
```
- 安卓反编译里的osskey是真的多，可以搜secret，但有些是直接key=，id=,这种可以直接正则搜\w{20,50}$
- 搭环境代码审计白盒测试的时候，开启mysql报错日志监控很重要，能发现一些隐蔽的盲注。
- https://regex101.com/    正则在线调试
- http://get-av.se7ensec.cn    Windows杀软在线对比辅助
- https://jsonwebtoken.io       jwt在线解码
- 小密圈最干的货都放在公众号吸引流量了，花几百块的进圈不太值得
- 工作原因，估计不会再更新了，整理别人的东西没太大意义。一年前，干了十年渗透的大佬跟我说这是真大牛写的文章https://www.freebuf.com/articles/neopoints/190895.html，现在回头看确实受益匪浅。特别是https://pentester.land/和推特搜索 #bugbountytips 能学到不少大佬挖洞的技巧。还有就是看乌云镜像和hackone的挖洞过程。
```


