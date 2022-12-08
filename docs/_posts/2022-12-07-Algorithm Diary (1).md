---
layout: post
title: "Algorithm Diary (1)"
date: 2022-12-07 17:28:00 -0000
categories: CATEGORY-1 CATEGORY-2
---
## 704. binary-search 
** Question:给定一个有`n`个元素的有序的整型数组`nums`和一个目标值`target`,写一个函数搜索`nums`中的`target`,如果目标值存在返回下标，否则返回`-1`。

### Gneral Thinking:

该题可使用二分法缩小查找边界，最终锁定目标值（需要注意的是边界的范围，这里只考虑范围为闭区间）。首先初始化两个指针`left`, `right`分别指向数组首位和末位并在后续的循环中作为区间左右边界。设置循环条件为 `while(i<=j)`(因为是闭区间，所以 `i == j` 是有意义的。当`i == j` 时，`mid = i = j`。此时再判断该位置元素是否为`target`)。之后进入循环，判断`target`是否:
- 在左半区间：即`target`不在`[mid,j]`区间内，所以将右边界设为`mid-1`。 
- 在右半区间：即`target`不在`[i,mid]`区间内，所以将左边界设置为`mid+1`。
- 等于`nums[mid]`:返回`mid`为答案。

### Solution: 
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

## 27. remove element 
** Question:给定一个数组'nums'和一个目标值`val`,原地移除所有数值等于val的元素，并返回移除后数组的新长度。要求空间复杂度为O(1)

### Gneral Thinking:

该题可以使用相向双指针，一个指针`left`从左往右遍历，另一个指针`right`从右往左。循环遍历的条件为while(left <= right),当指针相遇时，即`right == left`时退出循环。在遍历数组时，若左侧遍历到元素`nums[left]`等于val，此时，循环遍历右侧指针，直到`right`位置上的值不等于`val`时，交换两个位置上的值,再进行一次`right--`并判两个指针是否相遇。需要注意的是条件的判断，在处理完`nums[left] == val`这个条件之后不需要`left++`，因为在该位置上已经是一个新的元素，否则，在临近边界的时候，容易出现问题。

### Solution: 
```
    public int removeElement(int[] nums, int val) {
        int left = 0, right = nums.length - 1; 
        while(right >= 0 && nums[right] == val){
            right--;
        }
        while(left <= right){
            if(nums[left] == val){
                if(nums[right] == val){
                    right--;
                }else{
                    int tmp = nums[left];
                    nums[left] = nums[right];
                    nums[right] = tmp; 
                }
            }else{
                left ++;
            }
        }
        return left;
    }

```
