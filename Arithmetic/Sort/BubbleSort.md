

## 冒泡排序

*   [前言](#pre)

*   [冒泡思想](#idea)

*   [Code](#code)


<h3 id="pre">前言</h3>

如果一个数组中，只有一两个是无序的，冒泡排序比较适合


<h3 id="idea"></h3>


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
            
            for(int i=0; i < arrLength-1; i++){
            
                for(int j=0; j< arrLength-i-1; j++){
                
                    if(arr[j) > arr[j+1]){
                        
                        int temp = arr[j];
                        
                        arr[j] = arr[j+1];
                        
                        arr[j+1] = temp;
                    }
                }
            }
        
        }
        
    }
