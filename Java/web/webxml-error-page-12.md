
#web.xml 简介【12】

## error-page 配置介绍


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


        <!-- session会话设置-->
        <session-config>
            <session-timeout>60</session-timeout>
        </session-config>

        <!-- 扩展文件打开方式-->
        <mime-mapping>
            <extension>doc</extension>
            <mime-type>application/msword</mime-type>
        </mime-mapping>

        <!-- 默认打开页面 -->
        <welcome-file-list>
			<welcome-file>index.html</welcome-file>
			<welcome-file>index.jsp</webcome-file>
			<welcome-file>index.htm</welcome-file>
        </welcome-file-list>

        <!-- -->
        <error-page>
            <error-code>500</error-code>
            <location>/error.jsp</location>
        </error-page>

        <error-page>
            <exception-type>java.lang.NullException</exception-type>
            <location>/error.jsp</location>
        </error-page>

	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**


    <!--
    The error-page element contains a mapping between an error code
    or exception type to the path of a resource in the web application

    Used in: web-app
    -->
    <!ELEMENT error-page ((error-code | exception-type), location)>

    <!--
    The exception type contains a fully qualified class name of a
    Java exception type.

    Used in: error-page
    -->
    <!ELEMENT exception-type (#PCDATA)>

    <!--
    The location element contains the location of the resource in the web
    application relative to the root of the web application. The value of
    the location must have a leading `/'.

    Used in: error-page
    -->
    <!ELEMENT location (#PCDATA)>

    <!--
    The error-code contains an HTTP error code, ex: 404

    Used in: error-page
    -->
    <!ELEMENT error-code (#PCDATA)>


\<error-page>定义了当服务发生错误时，跳转的页面。有两种定义方案

方法一：根据错误码来跳转
\<error-code>元素节点写填写错误码，如404，500等
\<location>元素节点下填写跳转的路径

方法二：根据java异常类型来跳转
\<exception-type>元素节点下填写异常类
\<location>元素节点下填写跳转路径


***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【11】之welcome-file-list介绍](./webxml-welcome-file-list-11)

下一篇：[web.xml简介【13】之taglib介绍](./webxml-taglib-13)

