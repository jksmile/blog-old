


#web.xml 简介【2】

## login-config 配置介绍


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

		<login-config>
			……
		</login-config>

	</web-app>

login-config配置与需要与<security-constraint>元素节点下的<auth-constraint>配合使用。

***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【16】之security-constraint介绍](./webxml-security-constraint-16)

下一篇：[web.xml简介【18】之security-role介绍](./webxml-security-role-18)


