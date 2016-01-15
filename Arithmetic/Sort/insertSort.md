

## 【插入排序】直接插入排序

*   [前言](#pre)

*   [插排思想](#idea)

*   [Code](#code)


***


<h3 id="idea">快排思想</h3>

插入排序就是每一步都将一个待排数据按其大小插入到已经排序的数据中的适当位置，直到全部插入完毕

比如，以下是未排序的数组：

    | 4 | 3 | 5 | 1 | 2 |


先拿出第二个数【下标为1】 与 第一个数【下标为0】的数进行对比，如果第一个数大于第二个数，则需要将第二个数临时存储，将第一个数后移，然后将临时存储的数【原第二个数】插入前面的位置

    i = 1;
    
    | 4 |   | 5 | 1 | 2 |  int temp = arr[1];  
        
    |   | 4 | 5 | 1 | 2 |  arr[i] = arr[i-1];
    
    | 3 | 4 | 5 | 1 | 2 |  arr[i-1] = temp

接着指指针后移，将后面的数插入到i之前已经排序的序列

    i = 2;
        
    arr[i] = 5;
    
    arr[i] > arr[i-1] ? pass
        
    | 3 | 4 | 5 | 1 | 2 |  


继续指针后移，将后面的数插入到i之前已经排序的序列

    
    i = 3;
    
    arr[i] = 1;
    
    | 3 | 4 | 5 |   | 2 |   
    
    | 3 | 4 |   | 5 | 2 |  

    | 3 |   | 4 | 5 | 2 |

    |   | 3 | 4 | 5 | 2 |

    | 1 | 3 | 4 | 5 | 2 |


继续指针后移，将后面的数插入到i之前已经排序的序列
    
    i = 4;
    
    arr[i] = 2;
    
    | 1 | 3 | 4 | 5 |   |
    
    | 1 | 3 | 4 |   | 5 |
    
    | 1 | 3 |   | 4 | 5 |
    
    | 1 |   | 3 | 4 | 5 |

    | 1 | 2 | 3 | 4 | 5 |
    
<h3 id="code">Code</h3>

    
    public class InsertSort{
    
    
        public static void insertSortMethod(int[] arr){
            
            int arrLength = arr.length;
        
            if( arrLength == 0 ) return;
                    
            for( int i=1; i<arrLength; i++){

                if( arr[i-1] > arr[i] ){

                    int j = i;

                    int temp = arr[i];
        
                    while( j>0 && arr[j-1] > temp ){
                    
                        arr[--j] = arr[j-1];
                    }
                    
                    arr[j] = temp;
                }
            }
        }
    }
    
    

