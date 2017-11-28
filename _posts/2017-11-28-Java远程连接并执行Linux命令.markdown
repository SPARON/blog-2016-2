---
layout: post
title:  "Java远程连接并执行Linux命令"
date:   2017-11-28
categories: 编程
description: Java远程连接Linux系统并执行Linux命令
---

## 方式一

- Java通过调用ch.ethz.ssh2API远程连接Linux系统并执行linux命令。
- jar包下载地址：http://www.ganymed.ethz.ch/ssh2/


```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStream;  
import java.io.InputStreamReader;  
  
import ch.ethz.ssh2.Connection;  
import ch.ethz.ssh2.Session;  
import ch.ethz.ssh2.StreamGobbler;  
  
public class Basic  
{  
    public static void main(String[] args)  
    {  
        String hostname = "127.0.0.1";  
        String username = "joe";  
        String password = "joespass";  
  
        try  
        {  
            /* Create a connection instance */  
            Connection conn = new Connection(hostname);  
  
            /* Now connect */
            conn.connect();  
  
            /* Authenticate. 
             * If you get an IOException saying something like 
             * "Authentication method password not supported by the server at this stage." 
             * then please check the FAQ. 
             */  
            boolean isAuthenticated = conn.authenticateWithPassword(username, password);
            if (isAuthenticated == false)  
                throw new IOException("Authentication failed.");  
  
            /* Create a session */  
            Session sess = conn.openSession();  
            sess.execCommand("uname -a && date && uptime && who");  
            System.out.println("Here is some information about the remote host:");  
  
            /*  
             * This basic example does not handle stderr, which is sometimes dangerous 
             * (please read the FAQ). 
             */  
            InputStream stdout = new StreamGobbler(sess.getStdout());  
            BufferedReader br = new BufferedReader(new InputStreamReader(stdout));  
  
            while (true)  
            {  
                String line = br.readLine();  
                if (line == null)  
                    break;  
                System.out.println(line);  
            }  
  
            /* Show exit status, if available (otherwise "null") */  
            System.out.println("ExitCode: " + sess.getExitStatus());  
            /* Close this session */  
            sess.close();  
            /* Close the connection */  
            conn.close();  
        }  
        catch (IOException e)  
        {  
            e.printStackTrace(System.err);  
            System.exit(2);  
        }  
    }  
}  
```
## 方式二

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStream;  
import java.io.InputStreamReader;  
  
import com.jcraft.jsch.Channel;  
import com.jcraft.jsch.ChannelExec;  
import com.jcraft.jsch.JSch;  
import com.jcraft.jsch.JSchException;  
import com.jcraft.jsch.Session;  
  
  
  
public class ShellUtils {  
    private static JSch jsch;  
    private static Session session;  
  
      
    /** 
     * 连接到指定的IP 
     *  
     * @throws JSchException 
     */  
    public static void connect(String user, String passwd, String host) throws JSchException {  
        jsch = new JSch();  
        session = jsch.getSession(user, host, 22);  
        session.setPassword(passwd);  
          
        java.util.Properties config = new java.util.Properties();  
        config.put("StrictHostKeyChecking", "no");  
        session.setConfig(config);  
          
        session.connect();  
    }  
  
    /** 
     * 执行相关的命令 
     * @throws JSchException  
     */  
    public static void execCmd(String command, String user, String passwd, String host) throws JSchException {  
        connect(user, passwd, host);  
          
        BufferedReader reader = null;  
        Channel channel = null;  
  
        try {  
            while (command != null) {  
                channel = session.openChannel("exec");  
                ((ChannelExec) channel).setCommand(command);  
                  
                channel.setInputStream(null);  
                ((ChannelExec) channel).setErrStream(System.err);  
  
                channel.connect();  
                InputStream in = channel.getInputStream();  
                reader = new BufferedReader(new InputStreamReader(in));  
                String buf = null;  
                while ((buf = reader.readLine()) != null) {  
                    System.out.println(buf);  
                }  
            }  
        } catch (IOException e) {  
            e.printStackTrace();  
        } catch (JSchException e) {  
            e.printStackTrace();  
        } finally {  
            try {  
                reader.close();  
            } catch (IOException e) {  
                e.printStackTrace();  
            }  
            channel.disconnect();  
            session.disconnect();  
        }  
    }  
     
}  
```