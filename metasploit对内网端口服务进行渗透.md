`端口扫描`
    
    use auxiliary/scanner/portscan/syn
    use auxiliary/scanner/portscan/tcp
    
`Main`
    
    SMB版本识别：auxiliary/scanner/smb/smb_version 
    MSSQL信息收集：search mssql相关模块，如auxiliary/scanner/mssql/mssql_ping 查询mssql监听的端口，默认1433
    use auxiliary/scanner/mssql/mssql_login
    SSH版本信息：auxiliary/scanner/ssh/ssh_version
    FTP版本识别：auxiliary/scanner/ftp/ftp_version
    HTTP服务：auxiliary/scanner/http/http_header 返回相关header信息
    FTP服务：auxiliary/scanner/ftp/ftp_login  
    SSH服务：auxiliary/scanner/ssh/ssh_login
    Telnet服务：auxiliary/scanner/telnet/telnet_login 
    Mysql：auxiliary/scanner/mysql/mysql_login
    Mongodb：auxiliary/scanner/mongodb/mongodb_login
    redis：auxiliary/scanner/redis/redis_login
    auxiliary/scanner/redis/file_upload
    
