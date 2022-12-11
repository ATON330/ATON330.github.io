---
layout: post
title: "demo"
date: 2022-12-08 17:28:00 -0000
categories: CATEGORY-1 CATEGORY-2
---
## 977. squares of a sorted array 
**Question:给定一个按非递减顺序排序的整数数组`nums`，返回每个数字的平方组成的新数组，要求也按非递减顺序排序** 
 
### Gneral Thinking:
由于是递增数组且存在负数，所以该数组的平方应当是从第一个元素或最后一个元素向中间递减。因此可以使用双指针的方法，分别从第一个元素和最后一个元素开始相向遍历。每一次对比两个指针指向元素的平方大小，将指向较大的元素的指针加一/减一，并将该元素按顺序从新数组尾部开始放置。

### Solution: 
```
    public int[] sortedSquares(int[] nums) {
        int i = 0, j = nums.length - 1; 
        int[] res = new int[nums.length];
        int k = nums.length - 1;
        while(k>=0 && i <= j){
            int left = (int)Math.pow(nums[i],2);
            int right = (int)Math.pow(nums[j],2);
            if(left < right){
                res[k] = right;
                j--;
            }else{
                res[k] = left;
                i++;
            }
            k--;
        }
        return res;
    }
```
## 209. 长度最小的子数组
**Question:给定一个含有`n`个正整数的数组和一个正整数`s`，找出该数组中满足` 和>=s`的长度最小的连续子数组，并返回其长度。如果不存在，返回0** 
 
### Gneral Thinking:
该题的目标在寻找满足要求的最小长度数组，可以使用滑动窗口的方法通过遍历一次数组得到结果。遍历中每一轮都要计算已改元素为结尾的满足要求的最小长度数组。而改判断应当在满足条件后进行，所以应当首先增加数组长度，待数组的和`>=s`后，再通过`while`判断以目前元素为结尾的满足条件的最小长度数组

### Solution: 
```
    public int minSubArrayLen(int target, int[] nums) {
        int i = 0, subLength = Integer.MAX_VALUE, sum = 0, res = Integer.MAX_VALUE; 
        for(int j = 0; j < nums.length; j++){
            sum += nums[j];
            while(sum >= target){
                subLength = j - i + 1; 
                res = Math.min(subLength, res);
                sum -= nums[i];
                i++;
            }
        }
        return res == Integer.MAX_VALUE ? 0 : res;
    }
```
