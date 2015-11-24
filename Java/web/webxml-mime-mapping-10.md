
#web.xml 简介【10】

## mime-mapping 配置介绍


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

        <!-- -->
        <mime-mapping>
            <extension>doc</extension>
            <mime-type>application/msword</mime-type>
        </mime-mapping>

	</web-app>



**[web.xml文件范例](./webxml)中有如下一段描述：**


    <!--
    The mime-mapping element defines a mapping between an extension
    and a mime type.

    Used in: web-app
    -->
    <!ELEMENT mime-mapping (extension, mime-type)>

    <!--
        The extension element contains a string describing an
        extension. example: "txt"

        Used in: mime-mapping
        -->
    <!ELEMENT extension (#PCDATA)>

    <!--
    The mime-type element contains a defined mime type. example:
    "text/plain"

    Used in: mime-mapping
    -->
    <!ELEMENT mime-type (#PCDATA)>



\<mime-mapping>元素定义了扩展文件打开的方式【避免直接在浏览器中被打开】，此元素节点下有\<extension>,\<mime-type>两元素

\<extension>元素填写扩展文件的后缀名

\<mime-type>元素定义了打开的方式


***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml简介【9】之session-config介绍](./webxml-session-config-9)

下一篇：[web.xml简介【11】之welcome-file-list](./webxml-welcome-file-list-11)
