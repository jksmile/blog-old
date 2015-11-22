


#web.xml 简介

web.xml文件虽然不是一个web服务中所必须的，但有了web.xml后，可以减去代码中诸多注解

web.xml文件是用来初始化配置信息：比如Welcome页面、servlet、servlet-mapping、filter、listener、启动加载级别等

这里有一份[web.xml文件范例](./webxml)，接下来我们将根据范例里对web.xml配置的描述进行相关的示例讲解



*  [\<web-app>]()

    *   [\<security-constraint>](./webxml-security-constraint)

    *   [\<login-config>](./webxml-login-config)

    *   [\<display-name>](./webxml-display-name)





***


##根节点信息

每个xml文件都有定义它书写规则的Schema文件，也就是说javaEE的定义web.xml所对应的xml Schema文件中定义了多少种标签元素

web.xml中就可以出现它所定义的标签元素，也就具备哪些特定的功能

web.xml的模式文件是由Sun 公司定义的，每个web.xml文件的根元素为\<web-app>中，必须标明这个web.xml使用的是哪个模式文件

For Example：

    <?xml version="1.0" encoding="UTF-8"?>
    <web-app version="2.5"
    xmlns="http://java.sun.com/xml/ns/javaee"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
    http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">



    </web-app>


web.xml的模式文件中定义的标签并不是定死的，模式文件也是可以改变的。

一般来说，随着web.mxl模式文件的版本升级，里面定义的功能会越来越复杂，标签元素的种类肯定也会越来越多，但有些不是很常用的

我们只需记住一些常用的并知道怎么配置就可以了，但我还是想全面的了解下web.xml文件各种配置的作用


Let's start...

***

本篇所属：[java web篇](./Java/web/Index)

下一篇：[web.xml 简介【1】之security-constraint介绍](./webxml-security-constraint)
