

## 【选择排序】堆排序

*   [前言](#pre)

*   [思想](#idea)

*   [Code](#code)



<h3 id="pre">前言</h3>

***

    Waiting for update...




<h3 id="idea">思想</h3>

***

原数组arr如下：

    存储结构：
    | 8 | 3 | 6 | 4 | 1 | 2 | 5 | 7 |
    
    逻辑结构：
              8
            /   \
           3     6
          / \   / \ 
         4   1 2   5
        /  
       7

1.首先将原数据建成一个 **大顶堆**（大顶堆表示每个非叶子节点值大于其子节点值）,从最后一个非叶子节点开始进行,将大于父节点值的且是子节点中最大的子节点与父节点互换
    

    arr[3]在逻辑结构中为最后一个非叶子节点，与其子节点比较后：
              8 
            /   \
           3     6
          / \   / \ 
         7   1 2   5
        /  
       4    
    
    
    arr[2] 值大于其子节点值，不变：
              8 
            /   \
           3     6
          / \   / \ 
         7   1 2   5
        /  
       4    


    arr[1]与其子节点递归比较，结果：
              8 
            /   \
           7     6
          / \   / \ 
         3   1 2   5
        /  
       4    
        
              8 
            /   \
           7     6
          / \   / \ 
         4   1 2   5
        /  
       3    
    
    arr[0] 大于其子节点值，不变
    
    至此，无序的大顶堆已经建成
    
    
    
2.将堆顶与堆堆最后一个记录交换，除最后一个记录外，调整交换后的记录得到一个新的堆，然后继续堆顶与倒数第2个记录交换，进行调整... 依次进行！



    堆顶与最后一个记录进行交换，结果：
              3 
            /   \
           7     6
          / \   / \ 
         4   1 2   5
        /   
       8
    
    调整交换后的序列（除去最后1个元素）），结果：
              7 
            /   \
           4     6
          / \   / \ 
         3   1 2   5
        /   
       8        
    
    堆顶与倒数第2个元素交换，结果：
              5 
            /   \
           4     6
          / \   / \ 
         3   1 2   7
        /   
       8        
    
    调整交换后的序列（除去最后2个元素），结果：
              6 
            /   \
           4     5
          / \   / \ 
         3   1 2   7
        /   
       8        
        
    堆顶与倒数第3个元素交换，结果：
              2 
            /   \
           4     5
          / \   / \ 
         3   1 6   7
        /   
       8            
       
    调整交换后的序列（除去最后3个元素），结果：
              5 
            /   \
           4     2
          / \   / \ 
         3   1 6   7
        /   
       8

    堆顶与倒数第4个元素交换，结果：
              1 
            /   \
           4     2
          / \   / \ 
         3   5 6   7
        /   
       8            
       
    调整交换后的序列（除去最后4个元素），结果：
              4 
            /   \
           3     2
          / \   / \ 
         1   5 6   7
        /   
       8

    堆顶与倒数第5个元素交换，结果：
              1 
            /   \
           3     2
          / \   / \ 
         4   5 6   7
        /   
       8
       
    调整交换后的序列（除去最后5个元素），结果：
              3 
            /   \
           1     2
          / \   / \ 
         4   5 6   7
        /   
       8       
            
    堆顶与倒数第6个元素交换，结果：
              2 
            /   \
           1     3
          / \   / \ 
         4   5 6   7
        /   
       8       
        
    调整交换后的序列（除去最后6个元素），结果不变！
    
    
    堆顶与倒数第7个元素交换，结果：
              1 
            /   \
           2     3
          / \   / \ 
         4   5 6   7
        /   
       8        
    
    调整交换后的序列（除去最后7个元素），不用比了！结束！
    
    
                     
<h3 id="code">Code</h3>

***

    public class HeapSort{
    
        public static void main(String[] args) {
    
            int[] arr = {8,3,6,4,1,2,5,7};
    
            heapSort(arr);
    
        }
    
    
        public static void heapSort(int[] arr){
    
            if( arr.length == 0) return;
    
            int lastNodeIndex = ((arr.length-1)-1) >> 1;
    
    
            for (int i = lastNodeIndex; i>=0; i--){
    
                buildMaxHeap(arr,arr.length,i);
            }
    
    
            for(int j = arr.length-1; j>=0; j--){
    
                int temp = arr[0];
    
                arr[0] = arr[j];
    
                arr[j] = temp;
    
                buildMaxHeap(arr,j,0);
            }
    
        }
    
    
    
        private static void buildMaxHeap(int[] arr, int heapSize, int nodeIndex){
    
            int leftChildIndex = (nodeIndex << 1) + 1;
    
            int rightChildIndex = (nodeIndex << 1) + 2;
    
            int lastNodeIndex = nodeIndex;
    
            if( leftChildIndex < heapSize && arr[lastNodeIndex] < arr[leftChildIndex] ){
    
                lastNodeIndex = leftChildIndex;
            }
    
            if( rightChildIndex < heapSize && arr[lastNodeIndex] < arr[rightChildIndex] ){
    
                lastNodeIndex = rightChildIndex;
            }
    
            if( nodeIndex != lastNodeIndex){
    
                int temp = arr[nodeIndex];
    
                arr[nodeIndex] = arr[lastNodeIndex];
    
                arr[lastNodeIndex] = temp;
    
                buildMaxHeap(arr,heapSize,lastNodeIndex);
            }
        }
    
    }
    