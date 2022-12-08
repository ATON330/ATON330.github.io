---
layout: post
title: "Algorithm Diary (1)"
date: 2022-12-07 17:28:00 -0000
categories: CATEGORY-1 CATEGORY-2
---
# 704. binary-search 
**Question:给定一个`n`个元素的有序的整型数组'nums'和一个目标值`target`,写一个函数搜索`nums`中的`target`,如果目标值存在返回下标，否则返回`-1`。

## Gneral Thinking:

该题可使用二分法缩小查找边界，最终锁定目标值（需要注意的是边界的范围，这里只考虑范围为闭区间）。首先初始化两个指针`left`, `right`分别指向数组首位和末位并在后续的循环中作为区间左右边界。设置循环条件为 `while(i<=j)`(因为是闭区间，所以 `i == j` 是有意义的。当`i == j` 时，`mid = i = j`。此时再判断该位置元素是否为`target`)。之后进入循环，判断`target`是否:
- 在左半区间：即`target`不在`[mid,j]`区间内，所以将右边界设为`mid-1`。 
- 在右半区间：即`target`不在`[i,mid]`区间内，所以将左边界设置为`mid+1`。
- 等于`nums[mid]`:返回`mid`为答案。

##Solution: 
```
    public int search(int[] nums, int target) {
        int i = 0, j = nums.length - 1;
        while(i <= j){
            int mid = i + (j-i)/2;
            if(target > nums[mid]) {
                i = mid + 1;
            }else if (target <nums[mid]){
                j = mid - 1 ; 
            }else{
                return mid; 
            }
        }
        return -1;
    }
```
