

##最大子序列和的三种算法


*   [1.算法一](#ArithmeticA)
    *   [分析](#ArithmeticA-Analysis)
    *   [代码](#ArithmeticA-Code)
    *   [时间复杂度](#ArithmeticA-O)
*   [2.算法二](#ArithmeticB)
    *   [分析](#ArithmeticB-Analysis)
    *   [代码](#ArithmeticB-Code)
    *   [时间复杂度](#ArithmeticB-O)
*   [3.算法三](#ArithmeticC)
    *   [分析](#ArithmeticC-Analysis)
    *   [代码](#ArithmeticC-Code)
    *   [时间复杂度](#ArithmeticC-O)

------

<h3 id="ArithmeticA">1.算法一</h3>

<h4 id="ArithmeticA-Analysis"><span style="color:blue">●</span>分析</h4>


    示例序列X： 【1,-8,2,-1,5,-4,-3,4】

计算序列X中最大子序列的和，通过钛合金狗眼扫描序列X最大子序列Y为【2,-1,5】

如何找到序列Y的？最笨的方法莫过于两层循环对比


<h4 id="ArithmeticA-Code"><span style="color:blue">●</span>代码</h4> 



    public class MaxSubSequenceSum{

        public static int maxSubSequenceSum(int[] arr) {

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


     
<h4 id="ArithmeticA-O"><span style="color:blue">●</span>时间复杂度</h4> 

     
忽略初始化参数的单元时间，考虑长度为N的序列嵌套FOR循环： 
    
    N-1 N-1   N-1         N
     ∑ * ∑  =  ∑ (N-i) =  ∑ (N-i+1)
    i=0 j=i   i=0        i=1

    = N + (N-1) + ... + 1 = (N+1)N/2 = N^2/2 + N/2

    
    
**间复杂度为：T(N) = O(N^2)**


-----


<h3 id="ArithmeticB">2.算法二</h3>


<h4 id="ArithmeticB-Analysis"><span style="color:blue">●</span>分析</h4>

    示例序列X： 【1,-8,2,-1,5,-4,-3,4】
    
相对于算法一而言算法二对于这个问题很好的利用了递归思想，可以说是体现递归能力的极好范例！

算法二将采用分治策略，把一个问题分成两个相同的子问题，然后递归下去直到遇界得结果，而治则是对子问题的解进行整合，得到整个问题的解！

最大子序列可能在三处出现，出现在序列的左半部、右半部、位于左右半部之中。

        前半部分  |  后半部分
                 |
    1  -8  2  -1 | 5  -4  -3  4
                 |

前半部分最大子序列和为2，后半部分最大了序列和为5。

前半部从尾开始最大子序列【2，-1】和为1，后半部分从头开始最大子序列【5】是5，横跨两部分且通过中间的最大和为6。

所以在序列X中最大子序列是包含前、后两部分的元素，和为6。


<h4 id="ArithmeticB-Code"><span style="color:blue">●</span>代码</h4>

    public class MaxSubSequenceSum{

        public static int maxSubSequenceSum(int[] arr, int left, int right){

                if(left == right){

                    if(arr[left] > 0){

                        return arr[left];

                    }else{

                        return 0;
                    }
                }

                int center = (left + right)/2;

                int maxLeftSum = maxSubSequenceSum(arr,left,center);

                int maxRightSum = maxSubSequenceSum(arr,center+1,right);

                int leftX =0, leftTmp = 0;

                for(int i=center; i>=left; i--){

                    leftTmp += arr[i];

                    if(leftTmp > leftX) leftX = leftTmp;
                }

                int rightX = 0, rightTmp = 0;

                for(int i=center+1; i<=right; i++){

                    rightTmp += arr[i];

                    if(rightTmp > rightX) rightX = rightTmp;
                }


                return Math.max(Math.max(maxLeftSum,maxRightSum),leftX+rightX);
        }

        public static void main(String[] args){

            int[] arr={1,-8,2,-1,5,-4,-3,4};

            maxSubSequenceSum(arr,0,arr.length-1);
        }
    }



<h4 id="ArithmeticB-O"><span style="color:blue">●</span>时间复杂度</h4>

对于长度为N的序列，利用算法二需要的时间主要是递归两行代码。

对于N=1   T(N) = 1;

对于N>1   T(N) = 2T(N/2) + O(N) 【每次运行，多了一个判断的时间单元】

=>  由此可推导：

T(2) = 4 = 2 * 2

T(4) = 12 = 4 * 3

T(8) = 32 = 8 * 4

若 N=2^k => T(N)=N*(k+1)=N(logN + 1) = O(NlogN)


 **间复杂度为：T(N) = O(NlogN)**


------

<h3 id="ArithmeticC">3.算法三</h3>

<h4 id="ArithmeticC-Analysis"><span style="color:blue">●</span>分析</h4>

算法三是聪明算法的典型，是算法一的改进！

算法三只对数据进行一次扫描，一旦序列被读入处理就不需要被记忆，且读入多少都能给出已经读入序列的最大子序列和，像算法三的具有的这种特性又被称为联机算法。

最大子序列的起点不可能是负数，即任何负的子序列不可能是最优子序列的前缀，所以遇到负的序列就可以放弃掉，从重开始找大于当前序列和的序列


<h4 id="ArithmeticC-Code"><span style="color:blue">●</span>代码</h4>

    public class MaxSubSequenceSum{

        public static int maxSubSequenceSum(int[] arr){

            int result=0, tmp=0;

            for(int i=0; i<arr.length; i++){

                tmp += arr[i];

                if(tmp > result){

                    result = tmp;

                }else if(tmp < 0){

                    tmp = 0;
                }
            }

            return result;
        }

    }


<h4 id="ArithmeticC-O"><span style="color:blue">●</span>时间复杂度</h4>

算法三的时间复杂度不用钛合金狗眼都知道 T(N) = O(N)



-----

来自《数据结构与算法分析》


