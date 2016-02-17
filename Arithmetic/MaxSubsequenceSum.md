

最大子序列和三种算法对比
====================

*   [算法一](#ArithmeticA)
    *   [分析](#ArithmeticA-Analysis)
    *   [代码](#ArithmeticA-Code)
    *   [时间复杂度](#ArithmeticA-O)
*   [算法二](#ArithmeticB)
    *   [分析](#ArithmeticB-Analysis)
    *   [代码](#ArithmeticB-Code)
    *   [时间复杂度](#ArithmeticB-O)
*   [算法三](#ArithmeticC)
    *   [分析](#ArithmeticC-Analysis)
    *   [代码](#ArithmeticC-Code)
    *   [时间复杂度](#ArithmeticC-O)

------

<h3 id="ArithmeticA">算法一</h3>

<h4 id="ArithmeticA-Analysis">分析</h4>


    示例序列X： 【1,-8,2,-1,5,-4,-3,4】

计算序列X中最大子序列的和，通过钛合金狗眼扫描序列X最大子序列Y为【2,-1,5】

如何找到序列Y的？最笨的方法莫过于两层循环对比


<h4 id="ArithmeticA-Code">代码</h4> 



    public class MaxSubSequenceSum1 {

        public static int methodN2(int[] arr) {

            int result = 0;

            for (int i = 0; i < arr.length; i++) {

                int tmp = 0;

                for (int j = i; j < arr.length; j++) {

                    tmp += arr[j];

                    if (tmp > result) {

                        result = tmp;
                    }
                }
            }

            return result;
        }

    }


     
<h4 id="ArithmeticA-O">时间复杂度</h4> 

     
忽略初始化参数的单元时间，考虑长度为N的序列嵌套FOR循环： 
    
    N-1 N-1   N-1         N
     ∑ * ∑  =  ∑ (N-i) =  ∑ (N-i+1)
    i=0 j=i   i=0        i=1

    = N + (N-1) + ... + 1 = (N+1)N/2 = N^2/2 + N/2

    
    
**间复杂度为：T(N) = O(N^2)**


-----


<h3 id="ArithmeticB">算法二</h3>


<h4 id="ArithmeticB-Analysis">分析</h4>

    示例序列X： 【1,-8,2,-1,5,-4,-3,4】
    
相对于算法一而言算法二对于这个问题很好的利用了递归思想，可以说是体现递归能力的极好范例

算法二将采用分治策略，把一个问题分成两个相同的子问题，然后递归下去直到遇界得结果，而治则是对子问题的解进行整合，得到整个问题的解！

最大子序列可能在三处出现，出现在序列的左半部、右半部、位于左右半部之中。

        前半部分  |  后半部分
                 |
    1  -8  2  -1 | 5  -4  -3  4
                 |

前半部分最大子序列和为2，后半部分最大了序列和为5，