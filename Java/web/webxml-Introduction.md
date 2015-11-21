


#web.xml 简介

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

下一篇：[web.xml 简介【1】之security-constraint介绍](./webxml-Introduction1)
