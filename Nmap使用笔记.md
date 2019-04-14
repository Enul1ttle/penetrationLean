## Nmap常用操作
- 对目标进行路由跟踪`nmap --traceroute 192.168.0.105`
- C段在线状况`nmap -sP 192.168.0.100/24`
- 系统指纹识别`nmap -O 192.168.0.105`
- 开放端口对应的服务版本`nmap -sV 192.168.0.123`
- 探测防火墙状态`nmap -sF -T4 192.168.0.100`

## Nmap端口状态与含义
- open -->开放的，表示应用程序正在监听该端口，外部可以访问
- filtered --> 被过滤的，表示端口被防火墙或其他网络设备阻止，不能访问
- closed -->关闭的
- unfiltered -->未被过滤的，，表示Nmap无法确定端口状态，需要进一步探测
- open/filtered --> 开发的或被过滤的，Nmap不能识别
- closed/filtered -->关闭的或被过滤，Nmap不能识别

## Nmap漏洞扫描
- 漏洞脚本升级`nmap --script-updatedb`
- 应用弱口令探测`nmap --script=auth 192.168.0.105`
- 暴力破解攻击`nmap --script=brute 192.168.0.105`
- 扫描常见的漏洞`nmap --script=vuln 192.168.0.105`
- webdav远程执行漏洞扫描`nmap iis-buffer-overflow 192.168.0.105`
- IIS<7.5 尝试短文件漏洞目录文件扫描`nmap -p80 -script http-iis-short-name-brute 192.168.0.105`
- 针对目标主机使用所有脚本`nmap -T4 -A -sV -v3 -d -oATargetoutput --script all 192.168.0.105`

### Nmap Full Web Vulnerable Scan
- `mkdir /usr/share/nmap/scripts/vulscan`
- `cd /usr/share/nmap/scrripts/vulscan`
- `wget http://www.computec.ch/projekte/vulscan/download/nmap_nse_vulscan-2.0.tar.gz && tar xzf nmap_nse_vulscan-2.0.tar.gz`
- `nmap -sS -sV –script=vulscan/vulscan.nse target`
- `nmap -sS -sV –script=vulscan/vulscan.nse –script-args vulscandb=scipvuldb.csv target`
- `nmap -sS -sV –script=vulscan/vulscan.nse –script-args vulscandb=scipvuldb.csv -p80 target`
- `nmap -PN -sS -sV –script=vulscan –script-args vulscancorrelation=1 -p80 target`
- `nmap -sV –script=vuln target`
- `nmap -PN -sS -sV –script=all –script-args vulscancorrelation=1 target`

### 一些曾经遇到的问题
#### 配合proxychains4 nmap 扫描对方内网的时候出现：
```
netutil.cc:1351: int collect_dnet_interfaces(const intf_entry*, void*): Assertion `rc == 0' failed 
```
vi /etc/proxychains.conf 注释掉proxy_dns

扫描的时候一定要带上`-Pn`
