

#web.xml 简介【1】

## icon 配置介绍


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

	</web-app>



\<icon>元素包含\<small-icon>和\<large-icon>两个子元素.用来指定web站台中小图标和大图标的路径.


\<small-icon>元素应指向web站台中某个小图标的路径,大小为16 X 16 pixel,但是图象文件必须为GIF或JPEG格式,扩展名必须为:.gif或.jpg.


\<large-icon>元素应指向web站台中某个大图表路径,大小为32 X 32 pixel,但是图象文件必须为GIF或JPEG的格式,扩展名必须为; gif或jpg.





***

本篇所属：[java web篇](./Java/web/Index)

上一篇：[web.xml 介绍](./webxml-Introduction)

下一篇：[web.xml 简介【2】之diplay-name介绍](./webxml-display-name)
