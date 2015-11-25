
#web.xml 简介【7】

## listener 配置介绍


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


        <!-- 配置监听类-->
        <listener>
            <listener-class> org.springframework.web.context.ContextLoaderListener </listener-class>
        </listener>

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


	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**
	
	<!--
    The listener element indicates the deployment properties for a web
    application listener bean.

    Used in: web-app
    -->
    <!ELEMENT listener (listener-class)>
    
    <!--
    The listener-class element declares a class in the application must be
    registered as a web application listener bean. The value is the fully qualified classname of the listener class.


    Used in: listener
    -->
    <!ELEMENT listener-class (#PCDATA)>
    


\<listener>元素表示Web应用部署监听类的，此元素节点下有\<listener-class>元素

\<listener-class>元素下填写的监听类要实现Servlet监听接口。


关于servlet监听器方面的问题，移步：




***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【6】之filter介绍](./webxml-filter-6)

下一篇：[web.xml简介【8】之servlet介绍](./webxml-servlet-8)