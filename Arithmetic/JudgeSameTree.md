
#判断两二叉树是否相同

如何判断两二叉树对等？

二叉树遍历，然后递归，想到的大概思路就是这样的，但改来改去，感觉码的砖老不简洁

一定有更简洁的，最后终果不其然，真有最简洁的....


**Code**

    public class TreeNode{

           private int val;

           private TreeNode left;

           private TreeNode right;

    }

    public class Demo{

           public boolean isSameTree(TreeNode x, TreeNode y){

                  if(x != null && y != null){

                        if(x.val == y.val){
                              return (isSameTree(x.left,y.left) && isSameTree(x.right,x.right));

                         }

                  }else if(xTree == null && yTree == null){

                             return true;

                  }

                  return false;
           }

    }




**Perfect Code**

    public class Demo{

           public boolean isSameTree(TreeNode x, TreeNode y){

                  if(x == null && y == null) return true;

                  return x !=null && y != null && x.val == y.val && isSameTree(x.left,y.left) && isSameTree(x.right,y.right);

           }

    }



***

本篇所属：[算法篇](/Arithmetic/Index)



