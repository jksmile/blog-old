

#分解相加返回一位数

最小的往往受到欺负...  现在要写个function让规则如下：

一个非负int值，将此值各位数相加，如果结果小于两位数就返回，否则游戏继续。

For example:

给一个数：77  --->  7+7=14 >10   ---> 1+4 =5 <10   ---> return 5

Tips:
1. 首先想到的就是递归...


**Code**

    public class Demo{

            public int addDigits(int num){

                   if(num < 10) return num;

                   int newNum = num/10 + num%10;

                   return addDigits(newNum);

            }

    }



***

本篇所属：[算法篇](/Arithmetic/Index)
