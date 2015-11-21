

#数组中是否有两数之和等于目标值

Source Url:[原文链接](https://leetcode.com/problems/two-sum/)


Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9

Output: index1=1, index2=2


***

**分析**

numbers = {2,7,11,15}   找到数组中相加等于9的两值，输出其键值【键从1启始】

这里想到的最普通的方法肯定是双循环了

使用双循环后得到的时间复杂度T(n) = n!

有没有更好的方法？  答案是必然的

a + b = c   =>   c - a = b

现在c是给定的值，a在需要循环的值，b自然就是我们需要去找的差值

我们可以使用一个MAP来解决这个问题，通过MAP可以可以确定我们要找的差值


**Code**


    public class Solution {

        public int[] twoSum(int[] nums, int target) {

            int len = nums.length;

            if(len < 2) return;

            HashMap<Integer,Integer> map = new HaspMap<Integer,Integer>();

            for(int i=0; i<len; i++){

                if(map.contains(nums[i]){

                    return new int[](map.get(num[i])+1,i+1);

                }else{

                    map.put(target-nums[i],i);

                }
            }

            return null;
        }

    }


***

本篇所属：[算法篇](/Arthmetic/Index)