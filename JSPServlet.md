1、Tomcat9.0.8：   
1.1、目录结构：    
<table>
<tr><td>bin/</td><td>二进制可执行文件和脚本</td></tr>
<tr><td>common/</td><td>Catalina本身和web应用可加载的类目录</td></tr>
<tr><td>conf</td><td>配置文件目录</td></tr>
<tr><td>logs</td><td>日志目录</td></tr>
<tr><td>server/</td><td>服务器所需的类库目录</td></tr>
<tr><td>shared/</td><td>web app共享的类库</td></tr>
<tr><td>webapps/</td><td>Web应用所存放的目录</td></tr>
<tr><td>work/</td><td>Tomcat的工作目录（jsp产生的class文件）</td></tr>
<tr><td>temp/</td><td>存放临时产生的文件</td></tr>
</table>
1.2、Tomcat配置文件：            
conf/server.xml： 服务器的主配置文件            
conf/web.xml: 定义所有Web应用的配置（缺省的Servlet定义和MIME类型定义）                
conf/tomcat-user.xml： 定义了tomcat用户的信息      
1.3、Tomcat manager page:    
>401 Unauthorized:     
>><role rolename="manager-gui"/>
  <role rolename="manager-script"/>
  <role rolename="manager-jmx"/>
  <role rolename="manager-status"/>
  <role rolename="admin-gui"/>
  <role rolename="admin-script"/>
  <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status, admin-gui, admin-script"/>
