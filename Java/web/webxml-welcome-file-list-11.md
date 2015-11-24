
#web.xml 简介【11】

## welcome-file-list 配置介绍


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


	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**

	<!--
	The welcome-file-list contains an ordered list of welcome files
	elements.

	Used in: web-app
	-->
	<!ELEMENT welcome-file-list (welcome-file+)>

	<!--
    	The welcome-file element contains file name to use as a default
    	welcome file, such as index.html

    	Used in: welcome-file-list
    	-->
    	<!ELEMENT welcome-file (#PCDATA)>

\<welcome-file-list>元素定义了默认访问页，此元素节点下有一个或者多个\<welcome-file>元素

\<welcome-file>元素的定义是有顺序的，依次按顺序查找文件是否存在，存在则显示


***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【10】之session-mime-mapping介绍](./webxml-mime-mapping-10)

下一篇：[web.xml简介【12】之error-page介绍](./webxml-error-page-12)
