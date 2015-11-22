
#web.xml 简介【6】

## filter 配置介绍


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


	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**


	<!--
	Declares a filter in the web application. The filter is mapped to
	either a servlet or a URL pattern in the filter-mapping element, using
	the filter-name value to reference. Filters can access the
	initialization parameters declared in the deployment descriptor at
	runtime via the FilterConfig interface.

	Used in: web-app
	-->
	<!ELEMENT filter (icon?, filter-name, display-name?, description?,
	filter-class, init-param*)>


\<filter>元素声明filter的相关设定，[过滤器元素将一个名字与一个实现接口相关联](http://www.cnblogs.com/bukudekong/archive/2011/12/26/2302183.html)

\<filter>元素下有\<icon>,\<filter-name>,\<display-name>,\<description>,\<filter-class>,\<init-param>元素

其中\<icon>,\<display-name>,\<description>是可选元素

\<filter-name>元素定义当前filter名称,该名称在应用中必须唯一

\<filter-class>元素定义实现filter的类

\<init-param>元素下面的\<param-name>,\<param-value>定义了被初始化的参数键值对


## filter-mapping 配置介绍


\<filter-mapping>元素依赖\<filter>元素，定义了\<filter>后，\<filter-mapping>决定期所应用的servlet

\<filter-mapping>元素下有\<filter-name>和\<url-pattern>

\<filter-name> 即我们\<filter>元素下\<filter-name>的值

\<url-pattern> 填写我们filter-name所应用的url模式，如：/* 【对所有URL应用】



***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【5】之context-param介绍](./webxml-context-param)

下一篇：[web.xml简介【7】之context-param介绍](./webxml-context-param)