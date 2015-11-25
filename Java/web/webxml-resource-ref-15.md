
#web.xml 简介【15】

## resource-ref 配置介绍


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
            <taglib-uri> Taglib </taglib-uri>
            <taglib-location> /WEB-INF/tlds/MyTaglib.tld </taglib-location>
        </taglib>

        <!-- -->
        <resource-env-ref>
            <description>Just Test</description>
            <resource-env-ref-type> javax.jms.Queue </resource-env-ref-type>
            <resource-env-ref-name> jms/StockQueue </resource-env-ref-name>
        </resource-env-ref>

        <!-- -->
        <resource-ref>


        </resource-ref>

	</web-app>





**[web.xml文件范例](./webxml)中有如下一段描述：**


    <!--
    The resource-ref element contains a declaration of a web application's
    reference to an external resource. It consists of an optional
    description, the resource manager connection factory reference name,
    the indication of the resource manager connection factory type
    expected by the web application code, the type of authentication
    (Application or Container), and an optional specification of the
    shareability of connections obtained from the resource (Shareable or
    Unshareable).

    Used in: web-app

    Example:

        <resource-ref>
        <res-ref-name>jdbc/EmployeeAppDB</res-ref-name>
        <res-type>javax.sql.DataSource</res-type>
        <res-auth>Container</res-auth>
        <res-sharing-scope>Shareable</res-sharing-scope>
        </resource-ref>
    -->
    <!ELEMENT resource-ref (description?, res-ref-name, res-type, res-auth,
            res-sharing-scope?)>







***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【14】之resource-env-ref介绍](./webxml-resource-env-ref-14)

下一篇：[web.xml简介【16】之security-constraint介绍](./webxml-security-constraint-16)

