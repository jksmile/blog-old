
#求二叉树各路径结点之和并找出最大值的路径

最近没事将大学里的《数据结构》（严蔚敏，吴伟民著）一书重拾温习，受益颇多，才发现工作之中诸多经验问题都找到了理论支撑。

当时觉得没用的书，现在只能嘲笑当时得多low... 现在依然很low... －－！


**事件背景**

因实际工作中，遇到一个关于权重的问题，需要将数据关系中最大权重的路径找到，然后就想到了《数据结构》中的dfs...

此事勾起了我码砖的激情,让我本已平静的心再次荡漾...

为了简单说明这个问题，我就拿个二叉树的模型来叙述一下我要达成的目标


**Case**

        1
       / \
      2   3
     /\
    4  5

如图所见，一个二叉树，各结点值是int类型，现在要找出各结点之和最大的路径。

如图可知，此二叉树有三条路径：

    ［1,2,4]，［1,2,5]，［1,3]

结点之和最大的是［1,2,5]，我们最终的目标就是要找到这条路径！

怎么破？


**分析**

找出结点之和最大的路径，我们就不得不遍历二叉树了。

说到遍历二叉树，我们都知道有先序遍历(dlr)，中序遍历(ldr)，后序遍历(lrd)。

这里我们尝试先序遍历，我个人感觉先序遍历比较easy的解决这个问题... 个人感觉...



分析下先序遍历的路径：1->2->4->5->3

当发现到达叶子结点时，确认一条路径，并将这路径中各结点相加得到sum，然后退回至父结点再次寻找另其它叶子结点，重复之前的操作，并与上次的sum进行比较...

如此重复下去，直至所有路径都遍历完成，sum保存的就是结点之和最大的值，关键是如何保存sum的路径？

当然是栈咯...  栈顶叶子结点，栈底根结点，嗯！


**Code**


    public class TreeNode{


        private TreeNode leftTree;

        private int val;

        private TreeNode rightTree;

        //getter and setter.
    }




    public class FindPath{

        private static stack stack = new stack();


        private static TreeMap<integer,string> treeMap = new TreeMap<integer, string>();


        public static void findMaxValueOfPath(TreeNode tree){

            if(null == tree) return;

            stack.push(tree);

            if(tree.getLeftTree() == null && tree.getRightTree() == null){

                string s = "";

                int sum = 0;

                for(TreeNode tmp: stack){

                    s += tmp.getval() + "->";

                    sum += tmp.getval();

                }

                treeMap.put(sum,s);

                stack.pop();

            }else{

                findMaxValueOfPath(tree.getLeftTree());

                findMaxValueOfPath(tree.getRightTree());

    　　　　　　　stack.pop();
            }
        }
    }


***

本篇所属：[算法篇](/Arithmetic/Index)


