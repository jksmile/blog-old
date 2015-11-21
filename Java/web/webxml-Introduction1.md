


#web.xml 简介【1】

## security-constraint 配置介绍


	<?xml version="1.0" encoding="UTF-8"?>
		<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         	xmlns="http://java.sun.com/xml/ns/javaee"
         	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
         	http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
         	id="web" version="2.5”>

		<!— 资源强制安全配置 -->
		<security-constraint>
			……
		</security-constraint>

	</web-app>

有时候我们希望通过某些认证的用户才能请求某些资源时，我们可以有web.xml中<web-app>根节点下配置\<security-constraint>元素 <br />
security-constraint从字面上的意思就是说强制安全的意思，其实它也就是这个作用 <br />
接下来我们来看下\<security-constraint>元素的相关配置及作用：

	<security-constraint>

    	<display-name>SecuritySetting</display-name>


    	<web-resource-collection>
        	<web-resource-name>BaseResource</web-resource-name>

        	<description>BaseResource Desc</description>

        	<url-pattern>*.css</url-pattern>
        	<url-pattern>*.js</url-pattern>
        	<url-pattern>*.jsp</url-pattern>

        	<http-method>GET</http-method>
        	<http-method>POST</http-method>

    	</web-resource-collection>


		<auth-constraint>
			<description>baseproject</description>
			<role-name>role1</role-name>
		</auth-constraint>

		<user-data-constraint>
			<transport-guarantee>NONE</transport-guarantee>
		</user-data-constraint>

	</security-constraint>

###\<security-constraint>元素包括四大块

#### 1.\<display-name> <br />
    1.字面的意思是展示的名称，其实就是一个应用名称，没什么实质作用，可以理解为一个标识备注。<br />
    2.\<display-name> 元素可以有\<web-app>、\<security-constraint>、\<servlet>、\<filter>这些元素节点下使用 <br />
    3.\<display-name> 值并不唯一，所以在web.xml里可以设置相同的值。<br />

####2.\<web-resource-collection><br />
    1.字面的意思是网站资源集合,些元素是用来确定需要保护的资源，在<security-constraint>元素节点下，至少包含一个 <br />
    2.\<web-resource-collection>元素节点。 															 <br />
    3.\<web-resource-collection>一般包括以下几个节点元素：                                             <br />

       	<web-resource-name>
        网站资源名称

        <description>
        资源描述

        <url-pattern>
        URL模式，配置要保护的URL的规则，仅限于直接访问资源的URL，通过RequestDispatcher访问不受限 【*.JSP, *.CSS等等】

        <http-method>
        受保护的HTTP请求方法，如缺省表示保护所有方法【GET,POST,PUT,HEAD,TRACE,DELETE,OPTIONS】


####3.\<auth-constraint><br />
    1.字面上的意思是强迫认证，\<auth-constraint>元素会指出哪些角色会有上述受保护的资源的访问权限<br />
    2.此元素下包括两节点元素：<br />

        <role-name>
         角色名称

        <description>
         角色描述

这个角色从哪里来？ 在我们的tomcat安装目录有conf/tomcat-user.xml文件,有如下配置：

	<role rolename="tomcat"/>
	<role rolename="role1"/>
	<user username="tomcat" password="tomcat" roles="tomcat"/>
	<user username="both" password="tomcat" roles="tomcat,role1"/>
	<user username="role1" password="tomcat" roles="role1”/>

将设置在这里的用户，可以选择你想设置的可以作为<role-name>元素的值 <br />
e.g.  \<role-name> role1 \</role-name> 表示只有role1用户可以访问受保护的资源。

如果没有配置<auth-constraint>元素，表示任何身份的用户远的可以访问相应资源，换句话说没有配置此元素<br />
\<security-constraint>的配置是没有任何作用<br />
如果配置了\<auth-constraint>元素，但内容为空，表示所有身份用户都被禁止访问相应的受保护资源<br />


####4.\<user-data-contraint> <br />
     1.字面上的意思是用户数据限制，此元素指出在访问受保护资源时使用什么传输协议<br />
     2.此元素下面必须包含一个<transport-guarantee>元素和一个可选的<description>元素<br />
     3.\<transport-guarantee>元素有三个合法的值：NONE、INTEGRAL、CONFIDENTIAL<br />
     4.NONE对所有通讯协议不加限制，其它两个要求使用SSL<br />




