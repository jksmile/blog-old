
#web.xml 简介【8】

## servlet 配置介绍


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

		<!--  -->
		<servlet>
			<servlet-name>springmvc</servlet-name>
			<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
			<init-param>
				<param-name>contextConfigLocation</param-name>
				<param-value>/WEB-INF/dispatch.xml</param-value>
			</init-param>
			<load-on-startup>1</load-on-startup>
		</servlet>


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
    The servlet element contains the declarative data of a
    servlet. If a jsp-file is specified and the load-on-startup element is
    present, then the JSP should be precompiled and loaded.

    Used in: web-app
    -->
    <!ELEMENT servlet (icon?, servlet-name, display-name?, description?,
    (servlet-class|jsp-file), init-param*, load-on-startup?, run-as?, security-role-ref*)>

    <!--
    The servlet-class element contains the fully qualified class name
    of the servlet.

    Used in: servlet
    -->
    <!ELEMENT servlet-class (#PCDATA)>

    <!--
    The servlet-mapping element defines a mapping between a servlet
    and a url pattern

    Used in: web-app
    -->
    <!ELEMENT servlet-mapping (servlet-name, url-pattern)>



\<servlet>元素定义向servlet或JSP页面制定初始化参数或定制URL时，必须首先命名servlet或JSP页面。


\<servlet></servlet> 用来声明一个servlet的数据，主要有以下子元素：    
     
 \<servlet-name></servlet-name> 指定servlet的名称    

 \<servlet-class></servlet-class> 指定servlet的类名称    

 \<jsp-file></jsp-file> 指定web站台中的某个JSP网页的完整路径    

 \<init-param></init-param> 用来定义参数，可有多个init-param。在servlet类中通过getInitParamenter(String name)方法访问初始化参数    

 \<load-on-startup></load-on-startup>指定当Web应用启动时，装载Servlet的次序。    
 当值为正数或零时：Servlet容器先加载数值小的servlet，再依次加载其他数值大的servlet.    
 当值为负或未定义：Servlet容器将在Web客户首次访问这个servlet时加载它    


## servlet-mapping 配置介绍

\<servlet-mapping></servlet-mapping> 用来定义servlet所对应的URL，包含两个子元素    

\<servlet-name></servlet-name> 指定servlet的名称    

\<url-pattern></url-pattern> 指定servlet所对应的URL    



***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【7】之listener介绍](./webxml-listener-7)

下一篇：[web.xml简介【9】之session-config介绍](./webxml-session-config-9)
