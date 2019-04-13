## 内网渗透命令 
### 0x01常用命令
```
hostname #主机名
systeminfo #系统信息（所在域，开机时间，安装信息，补丁情况，系统版本）
set #环境变量
net user #查看默认用户
net view #显示当前域或工作组中计算机的列表
net localgroup #查看用户组
net localgroup Administrators #查看Administrators组所有用户(包括隐藏用户)
query user #查看当前会话（window7 64以上）
tasklist /v #显示当前进程和进程用户
net config workstation #查看当前登陆用户信息
net statistics workstation #查看主机开机时间
net share #查看共享文件夹
```
### 0x02 不常用的命令
```
whoami /all   查看Mandatory Label看我们是否过uac
net session    查看有没有远程连过来的session
cmdkey /l     看是否保存了登陆凭证.（凭据管理器）
echo %logonserver%  查看登陆域
net stitastics server  查看登陆时间
Wmic  能让攻击者大量利用来获取系统信息的系统自带工具
	wmic qfe list #获取补丁信息
Netsh  做端口转发
spn –l administrator 域内查某个用户spn记录
dsquery | nltest  域内信息收集
                                   --- RcoIl
```
## 自己收集的
### 0x01 常见的
```
taskkill /f /im cmd.exe  #结束cmd.exe

netstat -ano | find "14147"   #查找pid为14147的进程
netstat -ano | findstr "1444" #查找占用1444端口的程序

net user test abcd1234 /add  #添加用户名为test 密码为abcd1234的用户
net localgroup Administrators test /add  #将用户添加进管理组

query user   #查看在线用户
logoff id    #注销用户

rd/s/q    #盘符:\某个文件夹  （强制删除文件文件夹和文件夹内所有文件）
del/f/s/q   #盘符:\文件名  （强制删除文件，文件名必须加文件后缀名）


```
### 0x02 文件查找
```
dir c:\windows\system32\*.dll | find "res"  #查找指定目录c:\windows\system32\下所有含有res文件名的dll文件
WHERE /R c:\windows *.exe  #查找指定目录c:\windows 下所有的exe文件
wmic process get name,executablepath  #查看程序安装目录
```

### 0x03 文件打包
```
c:\progra~1\winrar\rar.exe a -r  D:\WebRoot\1.rar D:\Tomcat 9.0\web\ #将D:\Tomcat 9.0\web\目录下的所有文件打包为1.rar
fsutil volume diskfree d: #查看D盘使用情况：第一行-->可用字节数,第二行-->字节总数，第三行-->未用
```
### 0x04 开启3389
```
REG ADD HKLM\SYSTEM\CurrentControlSet\Control\Terminal" "Server /v fDenyTSConnections /t REG_DWORD /d 0 /f   #开启端口
REG query HKLM\SYSTEM\CurrentControlSet\Control\Terminal" "Server\WinStations\RDP-Tcp /v PortNumber          #查端口
```
### 0x05 net view 命令 6118 报错
环境：win 2008 x64
```
sc config Browser start= demand    #等于号后面是有一个空格的，这很重要
sc start  Browser                  #启动服务
```
