
## 看书心得
- 你工资5K就要找目标工资3K人员的作为突破口。
- 人是最大的漏洞。
- 修改自己上传文件夹的时间，能大大干扰对方
- 收集目标公司背景，比如将要目标被收购，发钓鱼邮件的时候就要精心构造一封裁员名单的邮件，相比员工都对其感兴趣
- 一定要多测试，钓鱼链接的稳定性。因为人就要一发现不对劲，很难再有第二次机会。
## Tips
- 注意查看网页注释,js等信息.可能含作者等信息,再继续对这些信息进行信息搜集.多注意公告栏,通知等信息.
- 根据发布的内容对命名模式推断
例如：发现一个viewuser.asp页面，然后就可以查找类似edituser.asp、adduser.asp和deleteuser.asp。如果/app/user目录被发现接着可以查找/app/admin 、/app/manager。之前搞的一个cx站，发现/weadmin/是后台目录，猜测管理员账号是weadmin，弱口令就进去了。
- 注意额外不常见的或自定义的HTTP头,比如：debug=False 、  Server:BIG-IP（ 负载均衡）
- 随手在网页后面加old、~、bak、copy、orig 如index.asp.old。如果是网站是iis7.5，尝试index.asp/.php 运气好能读取到源码(iis7.5解析漏洞)。
- 利用`User Agent Switcher`切换不同的`User Agent`然后访问同一个特定页面。这是因为很多的Web应用对于不同的`User-Agent`和`Referer`请求头会返回不同的内容。
- 火狐浏览器右键`View image info` 查看图片相关信息，有些编辑器上传点放在目录后面。
- 登录框的js源码会找到很多意外收获。很多靠接口的运行的网站，看源码和js比爆破目录稳得多。
