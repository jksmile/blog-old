

## 冒泡排序

*   [前言](#pre)

*   [冒泡思想](#idea)

*   [Code](#code)

***

<h3 id="pre">前言</h3>

如果一个数组中，只有一两个是无序的，冒泡排序比较适合



<h3 id="idea">冒泡思想</h3>

**算法稳定性**

冒泡排序就是把小的元素往前调或者把大的元素往后调。比较是相邻的两个元素比较，交换也发生在这两个元素之间。所以，如果两个元素相等，我想你是不会再无聊地把他们俩交换一下的；如果两个相等的元素没有相邻，那么即使通过前面的两两交换把两个相邻起来，这时候也不会交换，所以相同元素的前后顺序并没有改变，所以冒泡排序是一种稳定排序算法。


比如，以下是未排序的数组：

    | 4 | 3 | 5 | 1 | 2 |

    
经过第一轮对比排序：

    | 3 | 4 | 5 | 1 | 2 |
    
    | 3 | 4 | 1 | 5 | 2 |
    
    | 3 | 4 | 1 | 2 | 5 |
    
经过第二轮对比排序：
    
    | 3 | 1 | 4 | 2 | 5 |
    
    | 3 | 1 | 2 | 4 | 5 |
    
经过第三轮对比排序：

    | 1 | 3 | 2 | 4 | 5 |

    | 1 | 2 | 3 | 4 | 5 |


<h3 id="code"></h3>


    public class Demo{
    
        public static void main(String[] args){
        
            int[] arr = {10,7,9,1,8,5,2};
            
            bubbleSort(arr);
        
        }
        
        
        public static void bubbleSort(int[] arr){
        
            int arrLength = arr.length;
            
            for(int i=arrLength-1; i >0; --i){
            
                for(int j=0; j< i; ++j){
                
                    if(arr[j) > arr[j+1]){
                        
                        int temp = arr[j];
                        
                        arr[j] = arr[j+1];
                        
                        arr[j+1] = temp;
                    }
                }
            }
        
        }
        
    }
