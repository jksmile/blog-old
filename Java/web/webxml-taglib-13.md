
#web.xml 简介【13】

## taglib 配置介绍


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

        <!-- 定义错误页面跳转-->
        <error-page>
            <error-code>500</error-code>
            <location>/error.jsp</location>
        </error-page>

        <error-page>
            <exception-type>java.lang.NullException</exception-type>
            <location>/error.jsp</location>
        </error-page>

        <!-- -->
        <taglib>
            <taglib-uri> </taglib-uri>
            <taglib-location> </taglib-location>
        </taglib>

	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**


    <!--
    The taglib element is used to describe a JSP tag library.

    Used in: web-app
    -->
    <!ELEMENT taglib (taglib-uri, taglib-location)>

    <!--
    the taglib-location element contains the location (as a resource
    relative to the root of the web application) where to find the Tag
    Libary Description file for the tag library.

    Used in: taglib
    -->
    <!ELEMENT taglib-location (#PCDATA)>

    <!--
    The taglib-uri element describes a URI, relative to the location
    of the web.xml document, identifying a Tag Library used in the Web
    Application.

    Used in: taglib
    -->
    <!ELEMENT taglib-uri (#PCDATA)>



\<taglib>元素被用来描述JSP标签库信息




***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【12】之error-page介绍](./webxml-error-page-12)

下一篇：[web.xml简介【14】之]()

