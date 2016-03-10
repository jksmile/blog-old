

##awk命令学习


*   [1.前言](#preface)

*   [2.语法](#grammar)

*   [3.实践](#action)

***

<h3 class="blueJK" id="preface">1.前言</h3>

awk是linux下一个强大的文本分析工具，在统计日志生成报告完全胜任！awk逐行将文本读入，在默认情况下以空格为分隔符将一行内容进行分隔，然后再进行各种需要的处理。


我在使用awk时，很好奇为什么这个命令叫awk，然后去搜索了下：awk其名称得自于它的创始人 Alfred Aho 、Peter Weinberger 和 Brian Kernighan 姓氏的首个字母。


好吧，可以任性到用三个人名字首字母来命名！【人家三位可都是大拿!】。


awk目前有4个不同版本: awk、nawk、mawk和gawk，awk一般指gawk，gawk 是 AWK 的 GNU 版本。


**关于4种版本的由来：**

    awk:   最初在1 9 7 7年完成，1 9 8 5年发表了一个新版本的awk，它的功能比旧版本增强了不少,awk 能够用很短的程序对文档里的资料做修改、比较、提取、打印等处理,如果使用C 或P a s c a l 等语言编写程序完成上述的任务会十分不方便而且很花费时间，所写的程序也会很大;
    
    nawk： 在 20 世纪 80 年代中期，对 awk语言进行了更新，并不同程度地使用一种称为 nawk(new awk) 的增强版本对其进行了替换。许多系统中仍然存在着旧的awk 解释器，但通常将其安装为 oawk (old awk) 命令，而 nawk 解释器则安装为主要的 awk 命令，也可以使用 nawk 命令。Dr. Kernighan 仍然在对 nawk 进行维护，与 gawk 一样，它也是开放源代码的，并且可以免费获得;
    
    mawk： mawk 是 awk 编程语言的解释器。awk语言在多媒体数据文件以及文本的检索和处理，算法的原型设计和试验都有广泛的使用。mawk带给awk新的概念，它实现了在 《The AWK Programming Language》（Aho, Kernighan and Weinberger, The AWK Programming Language, Addison-Wesley Publishing, 1988.被认为是 AWK 手册。）中定义的 awk语言。mawk遵循 POSIX 1003.2 （草案 11.3）定义的 AWK 语言，包含了一些没有在AWK 手册中提到的特色，同时 mawk 提供一小部分扩展,另外据说mawk是实现最快的awk；
    
    gawk： 是 GNU Project 的awk解释器的开放源代码实现。尽管早期的 GAWK 发行版是旧的 AWK 的替代程序，但不断地对其进行了更新，以包含 NAWK 的特性;
    


**awk其实已经可以称为成为一种脚本语言了！**
 
一般我们使用awk多以命令行的方式，但它不仅仅如此简单，除了命令行的方式调用，它还可以以shell脚本方式和使用awk调用文件的方式来使用。

    1. 命令行方式
    
        [web@AY131126170354435ec9Z test]$ awk '{commands}' target-file
        
        
    2. shell脚本方式
     
        在shell脚本 #!/bin/sh  替换成 #!/bin/awk

        
    3. awk调用文件
    
        awk -f script-file target-file


***

<h3 class="blueJK" id="grammar">2.语法</h3>

awk可以通过man看一下awk的一些内置变量:

    Variable names with special meanings:
    
           CONVFMT
                  conversion format used when converting numbers (default %.6g)
                  转换时默认使用内存大小【默认6G】
    
           FS     regular expression used to separate fields; also settable by option -Ffs.
                  设置输入域分隔符，等价于命令行 -F选项
           
           NF     number of fields in the current record
                  浏览当前记录的域的个数
                    
           NR     ordinal number of the current record
                  当前的记录行
                        
           FNR    ordinal number of the current record in the current file
                  当前文件当前记录的行数
                    
           FILENAME
                  the name of the current input file
                  前当文件名
    
           RS     input record separator (default newline)
                  输入记录的分隔【默认新行】  
                
           OFS    output field separator (default blank)
                  输出字段的分隔【默认空格】
                    
           ORS    output record separator (default newline)
                  输出记录分隔【默认新行】
                    
           OFMT   output format for numbers (default %.6g)
                  输出格式的大小【默认6G】
    
           SUBSEP separates multiple subscripts (default 034)
                  分隔多个下标            
        
           ARGC   argument count, assignable
                  参数个数
    
           ARGV   argument array, assignable; non-null members are taken as filenames
                  参数数组
                    
           ENVIRON
                  array of environment variables; subscripts are names.
                  环境变量的数组，下标是名字



**For example:**

    [web@AY131126170354435ec9Z test]$ less A-access.log
    42.62.36.167--[16/Mar/2014:21:35:34]--"GET--/forum.php?mod=forumdisplay&fid=40&filter=heat&orderby=heats--HTTP/1.1"
    42.62.36.167--[16/Mar/2014:21:35:39]--"GET--/forum.php?mod=forumdisplay&fid=51&filter=typeid&typeid=1--HTTP/1.1"
    118.72.253.80--[16/Mar/2014:21:35:40]--"GET--/forum.php--HTTP/1.1"
    42.62.36.167--[16/Mar/2014:21:35:44]--"GET--/forum.php?mod=misc&action=postreview&do=against&tid=146&pid=327&hash=3cb1b968--HTTP/1.1"
    42.62.36.167--[16/Mar/2014:21:35:49]--"GET--/forum.php?mod=forumdisplay&fid=103&filter=heat&orderby=heats--HTTP/1.1"
    42.62.36.167--[16/Mar/2014:21:35:54]--"GET--/forum.php?mod=misc&action=postreview&do=support&tid=194&pid=479&hash=36420ed8--HTTP/1.1"
    42.62.36.167--[16/Mar/2014:21:35:59]--"GET--/forum.php?mod=misc&action=postreview&do=support&tid=73&pid=385&hash=63a632b3--HTTP/1.1"
    5.10.83.48--[16/Mar/2014:21:36:39]--"GET--/home.php?mod=space&uid=44&do=friend&view=me--HTTP/1.1"--1290
    66.249.75.237--[16/Mar/2014:21:36:50]--"GET--/thread-105-1-1.html--HTTP/1.1"
    66.249.75.231--[16/Mar/2014:21:40:12]--"GET--/thread-110-1-1.html--HTTP/1.1"

    [web@AY131126170354435ec9Z test]$ awk -F "--" '{print "fileName:" FILENAME "\t" "lineNumber:" NR "\t" "columnNum:" NF}'  A-access.log
    fileName:A-access.log   lineNumber:1    columnNum:5
    fileName:A-access.log   lineNumber:2    columnNum:5
    fileName:A-access.log   lineNumber:3    columnNum:5
    fileName:A-access.log   lineNumber:4    columnNum:5
    fileName:A-access.log   lineNumber:5    columnNum:5
    fileName:A-access.log   lineNumber:6    columnNum:5
    fileName:A-access.log   lineNumber:7    columnNum:5
    fileName:A-access.log   lineNumber:8    columnNum:5
    fileName:A-access.log   lineNumber:9    columnNum:5
    fileName:A-access.log   lineNumber:10   columnNum:5
    [web@AY131126170354435ec9Z test]$


***


<h3 class="blueJK" id="action">3.实践</h3>

**统计记录总行数**

    [web@AY131126170354435ec9Z test]$ awk '{count++} END {print "lineSum:" count}' A-access.log
    lineSum:10

    -------------------------------
    Todo: count为自定义变量【强大不？】

**查看访问的IP**


$0表示当前行所有域，$1表示当前行第一个域，$2表示当前行第二个域...

    [web@AY131126170354435ec9Z test]$ ls
    access.log
    
    [web@AY131126170354435ec9Z test]$ tail -fn1 access.log 
    66.249.75.231 [16/Mar/2014:21:40:12] "GET /thread-110-1-1.html HTTP/1.1"
    
    [web@AY131126170354435ec9Z test]$ awk '{print $1}' access.log 
    42.62.36.167
    42.62.36.167
    118.72.253.80
    42.62.36.167
    42.62.36.167
    42.62.36.167
    42.62.36.167
    5.10.83.48
    66.249.75.237
    66.249.75.231
    
    [web@AY131126170354435ec9Z test]$ awk 'BEGIN {print "access-ip"} {print $1} END {print "End"}' access.log                
    access-ip
    42.62.36.167
    42.62.36.167
    118.72.253.80
    42.62.36.167
    42.62.36.167
    42.62.36.167
    42.62.36.167
    5.10.83.48
    66.249.75.237
    66.249.75.231
    End
    [web@AY131126170354435ec9Z test]$ 


**使用--分隔符进行分隔**

    [web@AY131126170354435ec9Z test]$ tail -fn1 A-access.log 
    66.249.75.231--[16/Mar/2014:21:40:12]--"GET--/thread-110-1-1.html--HTTP/1.1"
    
    [web@AY131126170354435ec9Z test]$ awk -F "--" 'BEGIN {print "access-IP \t Date"} {print $1"\t"$2}' A-access.log      
    access-IP        Date
    42.62.36.167    [16/Mar/2014:21:35:34]
    42.62.36.167    [16/Mar/2014:21:35:39]
    118.72.253.80   [16/Mar/2014:21:35:40]
    42.62.36.167    [16/Mar/2014:21:35:44]
    42.62.36.167    [16/Mar/2014:21:35:49]
    42.62.36.167    [16/Mar/2014:21:35:54]
    42.62.36.167    [16/Mar/2014:21:35:59]
    5.10.83.48      [16/Mar/2014:21:36:39]
    66.249.75.237   [16/Mar/2014:21:36:50]
    66.249.75.231   [16/Mar/2014:21:40:12] 

