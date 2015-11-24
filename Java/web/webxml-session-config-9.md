
#web.xml 简介【9】

## session-config 配置介绍


	<?xml version="1.0" encoding="UTF-8"?>
		<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         	xmlns="http://java.sun.com/xml/ns/javaee"
         	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
         	http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
         	id="web" version="2.5”>

		<!-- 站点ICON图标 -->
		<icon>

            <smalle-icon> /static/img/smalle.jpg </smalle-icon>

            <large-icon> /static/img/large.jpg <//large-icon>

		</icon>


		<!-- 应用名称 -->
		<display-name> Web </display-name>


		<!-- 描述 -->
		<descriptioin> </description>


		<!-- 分布处处理 -->
		<distributable />


		<!-- 需要被初始化加载的容器配制文件 -->
		<context-param>
            <description> spring-context </description>
            <param-name> contextConfigLocation </param-name>
            <param-value> /WEB-INF/spring-root.xml </param-value>
		</context-param>


		<!-- 过滤元素 -->
		<filter>
			<filter-name> characterEncodingFilter </filter-name>
			<filter-class> org.springframework.web.filter.CharacterEncodingFilter </filter-class>
			<init-param>
				<param-name> encoding </param-name>
				<param-value> UTF-8 </param-value>
			</init-param>
			<init-param>
				<param-name> forceEncoding </param-name>
				<param-value> true </param-value>
			</init-param>
		</filter>

		<!-- 被过滤的范围 -->
		<filter-mapping>
			<filter-name>characterEncodingFilter</filter-name>
			<url-pattern>/*</url-pattern>
		</filter-mapping>


        <!-- -->
        <session-config>
            <session-timeout>60</session-timeout>
        </session-config>


	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**


    <!--
    The session-config element defines the session parameters for
    this web application.

    Used in: web-app
    -->
    <!ELEMENT session-config (session-timeout?)>

    <!--
    The session-timeout element defines the default session timeout
    interval for all sessions created in this web application. The
    specified timeout must be expressed in a whole number of minutes.
    If the timeout is 0 or less, the container ensures the default
    behaviour of sessions is never to time out.

    Used in: session-config
    -->
    <!ELEMENT session-timeout (#PCDATA)>


\<session-config>元素节点下定义了web应用的session参数，其下有元素<session-timeout>

\<session-timeout>元素定义了session会话的过期时间，单位为分钟，填写0或者小于0表示永不过期


***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【8】之servlet介绍](./webxml-servlet-8)

下一篇：[web.xml简介【10】之mime-mapping介绍](./webxml-mime-mapping-10)
