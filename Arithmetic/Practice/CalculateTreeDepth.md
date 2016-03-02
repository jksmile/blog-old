
#二叉树深度计算

最近没事就跟树杠上了，虽然不知道在实际使用中会以什么样的形式应用，但还是蛮有兴趣的去耍耍.

朋友去面试一公司，说问了一堆关于树的问题，其中有一个问题如下：

问：写一个快速的算法去求一个二叉树的深度。

For example:

如下二叉树，深度为3.

        1
       / \
      2   3
     /\
    4  5


**Tips:**
1. 递归遍历树；
2. 从叶子结点到根结点；


**Code**

     public class TreeNode{

            private int val;

            private TreeNode right;

            private TreeNode left;

     }


    public class MaxDepth{

                  public int findMaxDepth(TreeNode root){

                         if(root == null) return 0;

                         int x = findMaxDepth(root.left)+1;

                         int y = findMaxDepth(root.right)+1;

                         return Math.max(x,y);
                  }

    }



**网上看到一个更简洁的写法【赞！】：**


    public class MaxDepth{

              public int findMaxDepth(TreeNode root){

                   return (root==null)?0:Math.max(findMaxDepth(root.left)+1,findMaxDepth(root.right)+1);

              }

    }


***

本篇所属：[算法篇](/Arithmetic/Index)

