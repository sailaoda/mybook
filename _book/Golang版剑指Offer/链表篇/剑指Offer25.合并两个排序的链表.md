# 剑指Offer25.[合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

## 题目描述：

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

## 示例1：

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

## 限制：

```
0 <= 链表长度 <= 1000
```

## 解题思路：

**中心思想：因为有序，则利用双指针分别指向两条链表的表头，然后通过比较大小改变这些节点的指向即可。**

1. 利用一个头节点`head`简化合并过程。

## 算法代码：

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
    head := &ListNode {
        Val : 0 ,
        Next : nil ,
    }
    p := head 
    for l1 != nil && l2 != nil {
        if l1.Val <= l2.Val {
            p.Next = l1
            l1 = l1.Next 
        }else {
            p.Next = l2 
            l2 = l2.Next 
        }
        p = p.Next
    }

    if l1 != nil {
        p.Next = l1 
    }
    if l2 != nil {
        p.Next = l2
    }

    return head.Next
}
```

![image-20211018223252610](https://cdn.jsdelivr.net/gh/sailaoda/sai_img//img/3/image-20211018223252610.png)



