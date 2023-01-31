---
layout: post
title: "Algorithm Diary (4)"
date: 2022-01-31 17:28:00 -0000
categories: CATEGORY-1 CATEGORY-2
---
## 递归の奥义
**三要素：**
**1. 确定递归函数的参数和返回值：开始递归前需要确定好哪些参数将参与递归，哪个值是需要被返回的。**
**2. 确定终止条件：在每次递归时检查某参数是否已经符合终止条件。**
**3. 确定单层递归的逻辑。**

## 144.binary tree preorder traversal
**Question:给你二叉树的根节点 root ，返回它节点值的前序遍历。**

### Gneral Thinking:
**前序遍历**的顺序是中、左、右。题目要求将所有节点放入一个数组中。根据递归三要素，该题应当由以下三个步骤完成：
- 确定递归函数的参数和返回值：递归函数的参数应当包括二叉树需要处理的节点以及用来存放节点数值的`ArrayList`
- 确定终止条件：很显然，终止条件就是当该节点为根节点的时候。
- 确定每层递归的逻辑：因为是前序遍历所以先将中间节点放入数组，再放入左节点（进入下一层递归 `traversal(node.left,res)`）及右节点（进入下一层递归`traversal(node.right,res)`）
### Solution: 
```
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        traversal(root, res);
        return res;
    }

    public void traversal(TreeNode root, List<Integer> res){
        if(root == null) {return;}
        res.add(root.val);
        traversal(root.left, res);
        traversal(root.right,res);
    }
}
```

## 206. Reverse linkedlist
**Question:反转一个给定链表。**

### Gneral Thinking:
遍历链表，将每个元素的`next`指针断开并重新指向它前一个元素。
### Solution: 
```
public ListNode reverseList(ListNode head) {
        //ListNode dummy = new ListNode();
        //dummy.next = head; 
        //ListNode pre = dummy, cur = head;
        ListNode pre = null; 
        ListNode cur = head; 
        while(cur != null){
            ListNode next = cur.next; 
            cur.next = pre; 
            pre = cur; 
            cur = next; 
        }
        return pre;
```
