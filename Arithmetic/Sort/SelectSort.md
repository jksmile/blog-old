

## 【选择排序】直接选择排序

*   [前言](#pre)

*   [思想](#idea)

*   [Code](#code)

***

<h3 id="pre">前言</h3>

    Waiting for update...


<h3 id="idea">思想</h3>

比如，以下是未排序的数组：

    | 4 | 3 | 5 | 1 | 2 |
    
经过第1轮选择，找出最小值，放第1位

    int temp = arr[0]
    arr[1] < temp -> temp = arr[1]
    | 4 | 3 | 5 | 1 | 2 | 
      ↑   ↑
          
    arr[2] > temp -> temp
    | 4 | 3 | 5 | 1 | 2 |       
              ↑
              
    arr[3] < temp -> temp = arr[3]
    | 4 | 3 | 5 | 1 | 2 |
                  ↑
                  
    arr[4] > temp -> temp
    | 4 | 3 | 5 | 1 | 2 |
                      ↑
                        
    arr[3] = arr[0],arr[0] = temp 
    | 1 | 3 | 5 | 4 | 2 |  


继续第2轮选择，找出除首位外的最小值，放第2位

    int temp = arr[1]
    
    arr[2] > temp -> temp;
    | 1 | 3 | 5 | 4 | 2 |
          ↑   ↑

    arr[3] > temp -> temp;
    | 1 | 3 | 5 | 4 | 2 |
                  ↑
                  
    arr[4] < temp -> temp = arr[4]
    | 1 | 3 | 5 | 4 | 2 |
                      ↑
    
    arr[4] = arr[1]  arr[1] = temp
    | 1 | 2 | 5 | 4 | 3 |                      

     
继续第三轮选择，在未排序序列中找出最小值放第3位

    int temp = arr[2];
    arr[3] < temp -> temp = arr[3]
    | 1 | 2 | 5 | 4 | 3 |
              ↑   ↑
         
    arr[4] < temp -> temp =arr[4]
    | 1 | 2 | 5 | 4 | 3 |
                      ↑

    arr[4] = arr[2]  arr[2] = temp   
    | 1 | 2 | 3 | 4 | 5 |
                                   
继续第4轮选择，在未排序序列中找最小值放第4位
                                   
    int temp = arr[3]
    arr[4] > temp -> temp
    | 1 | 2 | 3 | 4 | 5 |
                  ↑   ↑
    
    arr[3] = temp
    | 1 | 2 | 3 | 4 | 5 |
    
    
    
         
<h3 id="code">Code</h3>


    public class Demo{
    
        public static void main(String[] args){
        
            int[] arr = {10,7,9,1,8,5,2};
            
            bubbleSort(arr);
        
        }
        
        
        public static void selectSort(int[] arr){
        
            int arrLength = arr.length;
            
            for(int i=0; i<arrLength; i++){
                
                int temp = arr[i];
                
                int position = i;
                
                for(int j=i+1; j< arrLength; j++){
                    
                    if( arr[j] < temp ){
                        
                        temp = arr[j];
                        
                        position = j;
                    }
                }
                
                arr[position] = arr[i];
                
                arr[i] = temp;
            }
        }
        
    }
