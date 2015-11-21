
#零后置，保持数字相对排序

近来无事，跑去leetcode上又转了转，脑袋完全不好使了。

EASY的题都想不明白了，看来是要生锈的节奏！

有个问题如下：

现在有一个整型数组 [1,4,0,8,5,0,0,3] 写个function将输出: [1,4,8,5,3,0,0,0]

将所有的0后置，结果保持相关数的相对顺序。

Note:

不可创建新数组；
最小操作数组；


怎么玩？突然觉得应该有个待定指针的想法。

分析下：

    1 4 0 8 5 0 0 3

A. 找到第一个0，在循环此数组时，第三次循环即可找到0.记录此时的下标为point.

【第3次循环期望结果】

    1 4 0 8 5 0 0 3
        ↑
       point

B. 继续循环，碰到非零的数，就将数填充到point处，然后point++

【第4次循环期望结果】

    1 4 8 0 5 0 0 3
          ↑
         point
【第5次循环期望结果】

    1 4 8 5 0 0 0 3
            ↑
          point

C. 继续循环，碰到零，直接PASS过

【第6次/第7次循环结果】

    1 4 8 5 0 0 0 3
            ↑
           point
【第8次循环结果】

    1 4 8 5 3 0 0 0
              ↑
            point


**Code**

    public class Demo{

		public void moveZero(int[] nums){

			int point = -1;

			for(int i=0; i<nums.length; i++){

				if(nums[i] !=0 && point != -1){

					nums[point] = num[i];

					nums[i] = 0;

					point++;

				 }else if( nums[i] == 0 && point == -1){

					point = i;
				 }
			 }
		 }
	 }
